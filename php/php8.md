## PHP8 新特性



2020年11月26日，PHP 8.0.0 发布。

php8 相比 php7 增加了一些新特性和一些不兼容项，在生产环境部署前，一定要先测试是否正常。



#### PHP Core 核心部分

- Named Arguments
  -  可命名参数
- Attributes 
  - 注解
- Constructor Property Promotion 
  - 构造器属性提升
- Union Types 
  - 联合类型
- Match Expression 
  - Match 表达式
- Nullsafe Operator 
  - Nullsafe 运算符
- Other new Features 
  - 其他新特性



### Named Arguments 可命名参数

PHP 8.0.0引入了命名参数作为现有位置参数的扩展。命名实参允许根据**形参名称**而不是**形参位置**向函数传递实参。这使得参数的意义自文档化，使参数的顺序无关，并**允许任意跳过默认值**。

通过在值前面加上**参数名和冒号**来传递命名参数。允许使用保留关键字作为参数名。参数名称必须是一个标识符，不允许动态指定。

```php
myFunction(paramName: $value);
array_foobar(array: $value);

// NOT supported. 不允许使用动态指定参数名称
function_name($variableStoringParamName: $value);

// 使用参数位置方式传参
array_fill(0, 100, 50);
// 使用命名参数,下面2种都可以
array_fill(start_index: 0, num: 100, value: 50);
array_fill(value: 50, num: 100, start_index: 0);
```



命名参数可以与位置参数组合。在这种情况下，命名参数必须在位置参数之后。也可以只指定函数的一些可选参数，而不考虑它们的顺序。

```php
htmlspecialchars($string, double_encode: false);
// Same as
htmlspecialchars($string, ENT_COMPAT | ENT_HTML401, 'UTF-8', false);
```



多次传递相同的参数会抛出错误异常。

```php
function foo($param) {}
foo(1, param: 2);
foo(param: 1, param:2);
```



### Attributes  注解

 语法

```php
<?php
// a.php
namespace MyExample;

use Attribute;

#[Attribute]
class MyAttribute
{
    const VALUE = 'value';

    private $value;

    public function __construct($value = null)
    {
        $this->value = $value;
    }
}

// b.php

namespace Another;

use MyExample\MyAttribute;

#[MyAttribute]
#[\MyExample\MyAttribute]
#[MyAttribute(1234)]
#[MyAttribute(value: 1234)]
#[MyAttribute(MyAttribute::VALUE)]
#[MyAttribute(array("key" => "value"))]
#[MyAttribute(100 + 200)]
class Thing
{
}

#[MyAttribute(1234), MyAttribute(5678)]
class AnotherThing
{
}
```



可以通过反射的 `getAttributes`方法获取到注解的内容



如何定义注解类？

> 虽然不是严格要求对每个注解都定义一个类，但是建议对每个注解都建一个类，这样在全局使用时，可以使用 use 引入。

```php
namespace Example;

use Attribute;

#[Attribute]
class MyAttribute
{
}


```



### Constructor Property Promotion 构造器属性提升

> `__construct()` 方法通常用于实例化类的时候，参数初始化
>
> PHP 8.0.0 开始允许直接在构造方法进行对象属性的初始化

```php
class A
{
    protected int $x;
    protected int $y;
    
    public function __construct(int $x, int $y = 0)
    {
        $this->x = $x;
        $this->y = $y;
    }
}

// PHP 8.0.0 开始可以简化成以下
class A 
{
    // 放在构造方法的属性将被复制到属性和参数
    public function __construct(protected int $x, protected int $y = 0)
    {
        
    }
}
```



PHP 类只有一个构造器，这时候如果需要多个构造器，可以通过静态方法的方式去进行构造

```php
class Product {

    private ?int $id;
    private ?string $name;

    private function __construct(?int $id = null, ?string $name = null) {
        $this->id = $id;
        $this->name = $name;
    }

    public static function fromBasicData(int $id, string $name): static {
        $new = new static($id, $name);
        return $new;
    }

    public static function fromJson(string $json): static {
        $data = json_decode($json);
        return new static($data['id'], $data['name']);
    }

    public static function fromXml(string $xml): static {
        // Put your own logic here.
        $data = convert_xml_to_array($xml);
        $new = new static();
        $new->id = $data['id'];
        $new->name = $data['name'];
        return $new;
    }
}

$p1 = Product::fromBasicData(5, 'Widget');
$p2 = Product::fromJson($some_json_string);
$p3 = Product::fromXml($some_xml_string);
```



### Union Types 联合类型

> 也称为泛型

- null，false 不能作为union type

- 冗余类型也不能作为union type
  - 每种类型只能出现一次
  - 如果使用了bool 类型， false 就不能出现
  - 如果使用了object 类型，就不能使用其他的类型
  - 如果使用了 [iterable](https://www.php.net/manual/en/language.types.iterable.php) , array 和 [Traversable](https://www.php.net/manual/en/class.traversable.php) 就不能使用

```php
function foo(): int|INT {} // Disallowed
function foo(): bool|false {} // Disallowed

use A as B;
function foo(): A|B {} // Disallowed ("use" is part of name resolution)

class_alias('X', 'Y');
function foo(): X|Y {} // Allowed (redundancy is only known at runtime)
```



- void 7.1.0 开始



- static  8.0.0 开始，必须返回相同类的实例





### Match Expression  match 表达式

```php
// php7
switch (8.0) {
  case '8.0':
    $result = "Oh no!";
    break;
  case 8.0:
    $result = "This is what I expected";
    break;
}
echo $result;
// Oh no!

// php8
echo match (8.0) {
  '8.0' => "Oh no!",
  8.0 => "This is what I expected",
}
// This is what I expected

```





### Nullsafe Operator  nullsafe 运算符

```php
// php7
$country =  null;

if ($session !== null) {
  $user = $session->user;

  if ($user !== null) {
    $address = $user->getAddress();
 
    if ($address !== null) {
      $country = $address->country;
    }
  }
}

// php8
$country = $session?->user?->getAddress()?->country;
```



### 字符串和数字的比较

```php
// php7
0 == 'foobar' // true

// php8
0 == 'foobar' // false
// 当数字和字符串比较时，PHP8 使用数字比较
    
```

