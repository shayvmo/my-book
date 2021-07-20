# 适配器模式（Adapter）

> 将一个类的接口转换成可应用的兼容接口。适配器使原本由于接口不兼容而不能一起工作的那些类可以一起工作

```php
interface BookInterface
{
    public function turnPage();

    public function open();

    public function getPage(): int;
}

class Book implements BookInterface
{
    /**
    * @var int
    */
    private $page;

    public function open()
    {
        $this->page = 1;
    }

    public function turnPage()
    {
        $this->page++;
    }

    public function getPage(): int
    {
        return $this->page;
    }
}

class EBookAdapter implements BookInterface
{
    protected $eBook;
    
    /**
    * @param EBookInterface $eBook
    */
    public function __construct(EBookInterface $eBook)
    {
        $this->eBook = $eBook;
    }

    /**
    * 这个类使接口进行适当的转换.
    */
    public function open()
    {
        $this->eBook->unlock();
    }

    public function turnPage()
    {
        $this->eBook->pressNext();
    }

    /**
    * 注意这里适配器的行为： EBookInterface::getPage() 将返回两个整型，除了 BookInterface
    * 仅支持获得当前页，所以我们这里适配这个行为
    *
    * @return int
    */
    public function getPage(): int
    {
        return $this->eBook->getPage()[0];
    }
}

interface EBookInterface
{
    public function unlock();
    
    public function pressNext();

    /**
    * 返回当前页和总页数，像 [10, 100] 是总页数100中的第10页。
    *
    * @return int[]
    */
    public function getPage(): array;
}

class Kindle implements EBookInterface
{
    /**
    * @var int
    */
    private $page = 1;

    /**
    * @var int
    */
    private $totalPages = 100;

    public function pressNext()
    {
        $this->page++;
    }

    public function unlock()
    {
    }

    /**
    * 返回当前页和总页数，像 [10, 100] 是总页数100中的第10页。
    *
    * @return int[]
    */
    public function getPage(): array
    {
        return [$this->page, $this->totalPages];
    }
}

// 测试代码
class AdapterTest extends TestCase
{
    public function testCanTurnPageOnBook()
    {
        $book = new Book();
        $book->open();
        $book->turnPage();

        $this->assertEquals(2, $book->getPage());
    }

    public function testCanTurnPageOnKindleLikeInANormalBook()
    {
        $kindle = new Kindle();
        $book = new EBookAdapter($kindle);

        $book->open();
        $book->turnPage();

        $this->assertEquals(2, $book->getPage());
    }
}
```

## 思考

适配器模式和策略模式，看起来有点类似，都是抽象出一个统一父类接口的，但是适配器模式，是兼容不能一起工作的类

而策略模式则是切换不同的处理策略，使算法和客户端分开。
