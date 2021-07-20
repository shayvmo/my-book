# 面向对象中的SOLID原则

【编辑于】2021年7月20日 15:51

[https://learnku.com/php/t/28922](https://learnku.com/php/t/28922)

[https://blog.csdn.net/houzhizhen/article/details/79993880](https://blog.csdn.net/houzhizhen/article/details/79993880)

> S.O.L.I.D 是 面向对象设计 (OOD) 的 5 个准则的首字母缩写 ，这些准则是由 Robert C. Martin 提出的，他更为人所熟知的名字是 Uncle Bob。

> 这些准则使得开发出易扩展、可维护的软件变得更容易。也使得代码更精简、易于重构。同样也是敏捷开发和自适应软件开发的一部分。



## 面向对象编程和面向对象设计的五个原则

罗伯特·C·马丁在 21 世纪早期引入了名为「SOLID」的设计原则，指代了面向对象编程和面向对象设计的五个基本原则：

- 单一职责原则（**S**ingle Responsibility Principle）
- 开放封闭原则（**O**pen Closed Principle）
- 里氏替换原则（**L**iskov Substitution Principle）
- 接口隔离原则（**I**nterface Segregation Principle）
- 依赖反转原则（**D**ependency Inversion Principle）



### 单一职责原则

规定一个类有且仅有一个理由使其改变。

示例代码：

当存储订单的载体，或者验证规则改变时，orderProcessor 也要跟着改变，这时候就显得不够灵活，可以拆分出一个repo ,通过注入的方式，把职责分离出去

```php
class OrderProcessor 
{

    public function __construct(BillerInterface $biller)
    {
        $this->biller = $biller;
    }

    public function process(Order $order)
    {
        $recent = $this->getRecentOrderCount($order);

        if($recent > 0)
        {
            throw new Exception('Duplicate order likely.');
        }

        $this->biller->bill($order->account->id, $order->amount);

        DB::table('orders')->insert(array(
            'account'    =>    $order->account->id,
            'amount'    =>    $order->amount,
            'created_at'=>    Carbon::now()
        ));
    }

    protected function getRecentOrderCount(Order $order)
    {
        $timestamp = Carbon::now()->subMinutes(5);
        return DB::table('orders')->where('account', $order->account->id)
                                                ->where('created_at', '>=', $timestamps)
                                                ->count();
    }

}

// 分离职责
class OrderRepository 
{

    public function getRecentOrderCount(Account $account)
    {
        $timestamp = Carbon::now()->subMinutes(5);
        return DB::table('orders')->where('account', $account->id)
                                                ->where('created_at', '>=', $timestamp)
                                                ->count();
    }

    public function logOrder(Order $order)
    {
        DB::table('orders')->insert(array(
            'account'    =>    $order->account->id,
            'amount'    =>    $order->amount,
            'created_at'=>    Carbon::now()
        ));
    }

}

// 注入
class OrderProcessor {

    public function __construct(BillerInterface $biller, OrderRepository $orders)
    {
        $this->biller = $biller;
        $this->orders = $orders;
    }

    public function process(Order $order)
    {
        $recent = $this->orders->getRecentOrderCount($order->account);

        if($recent > 0)
        {
            throw new Exception('Duplicate order likely.');
        }

        $this->biller->bill($order->account->id, $order->amount);

        $this->orders->logOrder($order);
    }
}
```

#### 核心

单一职责原则的核心并不仅仅是让代码变短，而是要写出职责更加明确、方法更加内聚的类，所以要确保类里面所有的方法都隶属于该类的职责之内。在构建一个小巧、清晰且职责明确的类库以后，我们的代码会更加解耦，更容易测试，并且更易于修改。


### 开放封闭原则

> 开放封闭原则，又称开闭原则，规定代码对扩展是开放的，对修改是封闭的。


基于上述的代码，如果订单验证有多个验证规则，这段代码就会随着规则修改而修改，它对修改时开放的，这就违反了开放封闭原则。通过一个订单验证interface，去定义不同的规则，在orderProcessor 使用注入规则的方式，达到拓展开放，内部修改是封闭的。

```php
interface OrderValidatorInterface 
{
    public function validate(Order $order);
}

class RecentOrderValidator implements OrderValidatorInterface 
{

    public function __construct(OrderRepository $orders)
    {
        $this->orders = $orders;
    }

    public function validate(Order $order)
    {
        $recent = $this->orders->getRecentOrderCount($order->account);
        if ($recent > 0)
        {
            throw new Exception('Duplicate order likely.');
        }
    }
}

class OrderProcessor 
{
    public function __construct(BillerInterface $biller, OrderRepository $orders, array $validators = array())
    {
        $this->biller = $bller;
        $this->orders = $orders;
        $this->validators = $validators;
    }
    
    public function process(Order $order)
    {
        foreach($this->validators as $validator)
        {
            $validator->validate($order);
        }
    
        // Process valid order...
    }
}

// 我们在服务容器中注册 OrderProcessor 类：
$this->app->bind('OrderProcessor', function($app)
{
    return new OrderProcessor(
        $app->make('BillerInterface'),
        $app->make('OrderRepository'),
        [
            $app->make('RecentOrderValidator'),
            $app->make('SuspendedAccountValidator'),
        ]
    );
});

```

### 里氏替换原则

一个抽象的任意实现都可以在声明该抽象的地方替换它。

通俗点说就是：如果一个类使用了某个接口的实现，那么一定可以通过该接口的其它实现来替换它，不用做出任何修改。

> 里氏替换原则规定对象可以被其子类的实例所替换，并且不会影响到程序的正确性。

```php
class AreaCalculator {

    protected $shapes;

    public function __construct($shapes = array()) {
        $this->shapes = $shapes;
    }

    public function sum() {
        // logic to sum the areas
    }

    public function output() {
        return implode('', array(
            "",
                "Sum of the areas of provided shapes: ",
                $this->sum(),
            ""
        ));
    }
}

class VolumeCalculator extends AreaCalulator {
    public function construct($shapes = array()) {
        parent::construct($shapes);
    }

    public function sum() {
        // logic to calculate the volumes and then return and array of output
        return array($summedData);
    }
}
```

### 接口隔离原则

接口隔离原则规定，不应该强制接口的实现依赖于它不使用的方法。

在实际操作中，这个原则要求接口必须粒度很细，且专注于一个领域。

```php
// 例如计算形状的体积和面积
interface ShapeInterface {
    public function area();
    public function volume();
}

// 平面没有体积，这时候，就需要拆分这个interface
interface ShapeInterface {
    public function area();
}

interface SolidShapeInterface {
    public function volume();
}
```

### 依赖反转原则

它规定高层次的代码不应该依赖低层级的代码。

换句话说，高层次的代码应该依赖抽象接口，抽象接口就像是「中间人」一样，负责连接着高层次和低层次代码。

这个原则的另一层意思是，抽象接口不应该依赖具体实现，但具体实现应该依赖抽象接口。

` interface `的使用

```php
// 将依赖的MySQLConnection 具体实现，改成依赖抽象接口
class PasswordReminder
{
    private $dbConnection;

    public function __construct(MySQLConnection $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}

interface DBConnectionInterface
{
    public function connect();
}

class MySQLConnection implements DBConnectionInterface
{
    public function connect() {
        return "Database connection";
    }
}

class PasswordReminder
{
    private $dbConnection;

    public function __construct(DBConnectionInterface $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}
```



---

## 拓展



### 迪米特法则

也称最少知识原则，一个类对其他类知道的越少越好



### 合成复用原则

优先使用组合或者聚合的方式来关联类，其次才是使用继承