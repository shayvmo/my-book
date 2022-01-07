# 外观（门面）模式（Facade）

> 提供一个统一的接口，用来访问子系统中的一群接口，从而让子系统更容易使用。


```php

class SubSystem
{
    public function turnOnTV()
    {
        echo 'turnOnTV()';
    }

    public function setCD(string $cd)
    {
        echo "setCD( " . $cd . " )";
    }

    public function startWatching()
    {
        echo 'startWatching()';
    }
}

class Facade
{
    private $subSystem;

    public function __construct()
    {
        $this->subSystem = new SubSystem();
    }
    
    public function watchMovie()
    {
        $this->subSystem->turnONTV();
        $this->subSystem->setCD("a movie");
        $this->subSystem->startWatching();
    }
    
}

$facade = new Facade();
$facade->watchMovie();

```


## 设计原则

最少知识原则：只和你的密友谈话。也就是说客户对象所需要交互的对象应当尽可能少。
