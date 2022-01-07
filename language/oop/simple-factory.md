# 简单工厂模式 (Simple Factory)

在创建一个对象时，不向客户端暴露内部细节

示例1:

```php
class SimpleFactory
{
    public function createBicycle(): Bicycle
    {
        return new Bicycle();
    }
}

class Bicycle
{
    public function show()
    {
        return 'this is Bicycle class.';
    }
}
```

用法
```php
$factory = new SimpleFactory();
$bicycle = $factory->createBicycle();
echo $bicycle->show();
```

示例2：

```php
interface Vehicle
{
    public function driveTo(string $destination);
}

class Bicycle implements VehicleInterface
{
    public function driveTo($destination)
    {
    }
}

class Scooter implements VehicleInterface
{
    public function driveTo($destination)
    {
    }
}


class SimpleFactory
{
    protected $typeList;

    public function __construct()
    {
        $this->typeList = [
            'bicycle' => __NAMESPACE__ . '\Bicycle',
            'other' => __NAMESPACE__ . '\Scooter',
        ];
    }

    public function createVehicle(string $type): Vehicle
    {
        if (!array_key_exists($type, $this->typeList)) {
            throw new \InvalidArgumentException("$type is not valid vehicle");
        }
        $className = $this->typeList[$type];

        return new $className();
    }
}
```
