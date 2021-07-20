# 注册模式（Registry）

> 注册模式（Registry）也叫做注册树模式，注册器模式。注册模式为应用中经常使用的对象创建一个中央存储器来存放这些对象 —— 通常通过一个只包含静态方法的抽象类来实现（或者通过单例模式）

```php
abstract class Registry
{
    const LOGGER = 'logger';

    private static $storedValue = [];

    public static function set(string $key, $value)
    {
        self::$storedValue[$key] = $value;
    }

    public static function get(string $key)
    {
        return self::$storedValue($key);
    }

}

// 测试代码
class RegistryTest extends \PHPUnit_Framework_TestCase
{

    public function testSetAndGetLogger()
    {
        Registry::set(Registry::LOGGER, new \StdClass());

        $logger = Registry::get(Registry::LOGGER);
        $this->assertInstanceOf('StdClass', $logger);
    }
}
```

## 例子

Yii 框架：CWebApplication 具有全部应用程序组件，例如 CWebUser，CUrlManager 等。
