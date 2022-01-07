# 工厂方法 (Factory Method)

定义了一个创建对象的接口，但由子类决定要实例化哪个类。工厂方法把实例化操作推迟到子类。

```php
abstract class FactoryMethod
{
    const BICYCLE = 'bicycle';
    abstract protected function createVehicle(string $type);

    public function create($type)
    {
        $obj = $this->createVehicle($type);
        $obj->setColor('white');
        return $obj;
    }
}

class Factory extends FactoryMethod
{
    // 交给子类去实例化对象，此处也使用了简单工厂
    protected function createVehicle(string $type)
    {
        switch ($type) {
            case parent::BICYCLE:
                return new Bicycle();
                break;
            default:
                throw new \InvalidArgumentException("$type is not a valid vehicle");
        }
    }
}

interface VehicleInterface
{
    public function setColor(string $color);
}

class Bicycle implements VehicleInterface
{
    protected $color;

    public function setColor(string $color)
    {
        $this->color = $color;
    }
}

```
