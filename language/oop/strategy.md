# 策略模式 (Strategy)

定义一系列算法，封装算法，并且它们可以互换。

策略模式使得算法和客户端独立。

```php
// 算法抽象
interface GoStrategyInterface
{
    public function go();
}

// 具体算法
class CarStrategy implements GoStrategyInterface
{
    public function go()
    {
        echo 'go by car';
    }
}

// 具体算法
class BusStrategy implements GoStrategyInterface
{
    public function go()
    {
        echo 'go by bus';
    }
}

class Train
{
    protected $go_strategy;

    public function __construct()
    {
    }

    // 设置算法
    public function setStrategy(GoStrategyInterface $goStrategy)
    {
        $this->go_strategy = $goStrategy;
    }

    public function go()
    {
        if (is_null($this->go_strategy)) {
            throw new \Exception('未设置策略');
        }
        $this->go_strategy->go();
    }
}

$obj = new Train();
$obj->setStrategy(new CarStrategy());
$obj->go();// go by car
$obj->setStrategy(new BusStrategy());
$obj->go();// go by bus
```
