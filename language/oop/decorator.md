# 装饰模式（Decorator）

> 为类示例动态增加新的方法

## 例子

设计不同种类的饮料，饮料可以添加配料，比如可以添加牛奶，并且支持动态添加新配料。

每增加一种配料，该饮料的价格就会增加，要求计算一种饮料的价格。

```php
interface DrinkInterface
{
    public function cost();
}

class Juice implements  DrinkInterface
{
    public function cost()
    {
        return 5;
    }
}

class Milk implements DrinkInterface
{
    public function cost()
    {
        return 6;
    }
}

abstract class MatchDecorator implements DrinkInterface
{
    protected $drink;

    public function __construct(DrinkInterface $drink)
    {
        $this->drink = $drink;
    }
}

// 芋圆
class Yuyuan extends MatchDecorator
{
    const PRICE = 2;

    public function cost()
    {
        return self::PRICE + $this->drink->cost();
    }
}

// 红豆
class Hongdou extends MatchDecorator
{
    const PRICE = 3;

    public function cost()
    {
        return self::PRICE + $this->drink->cost();
    }
}

$milk = new Milk();
$milk = new Yuyuan($milk);
$milk = new Hongdou($milk);
return $milk->cost();// 6 + 2 + 3 = 11

```

## 思考

满足开闭原则

当需要不断加配料时，不用去调整饮料的代码
