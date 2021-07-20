# 原型模式（Prototype）

> 相比正常创建一个对象 (new Foo () )，首先创建一个原型，然后克隆它会更节省开销。

## 例子

大数据量 (例如：通过 ORM 模型一次性往数据库插入 1,000,000 条数据)


```php
abstract class BookPrototype
{
    protected $title;
    
    protected $category;

    abstract public function __clone()
    {   

    }

    public function getTitle(): string
    {
        return $this->title;
    }

    public function setTitle($title)
    {
        $this->title = $title;
    }
    
}

class BarBookPrototype extends BookPrototype
{
    protected $category = 'Bar';
    
    public function __clone()
    {

    }
}

class FooBookPrototype extends BookPrototype
{
    /**
    * @var string
    */
    protected $category = 'Foo';

    public function __clone()
    {

    }
}

class PrototypeTest extends TestCase
{
    public function testCanGetFooBook()
    {
        $fooPrototype = new FooBookPrototype();
        $barPrototype = new BarBookPrototype();

        for ($i = 0; $i < 10; $i++) {
            $book = clone $fooPrototype;
            $book->setTitle('Foo Book No ' . $i);
            $this->assertInstanceOf(FooBookPrototype::class, $book);
        }

        for ($i = 0; $i < 5; $i++) {
            $book = clone $barPrototype;
            $book->setTitle('Bar Book No ' . $i);
            $this->assertInstanceOf(BarBookPrototype::class, $book);
        }
    }
}
```

## 思考

当对象被复制后，PHP 5 会对对象的所有属性执行一个浅复制（shallow copy）

所有的引用属性 仍然会是一个指向原来的变量的引用
