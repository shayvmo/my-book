# 单例模式( Singleton )

确保一个类只有一个实例，并提供该实例全局访问

```php
final class Singleton
{
    private static $instance;

    public static function getInstance(): Singleton
    {
        if (null === static::$instance) {
            static::$instance = new static();
        }
        return static::$instance;
    }

    // 不允许外部创建实例
    private function __construct()
    {

    }

    // 防止实例被克隆
    private function __clone()
    {

    }

    // 防止反序列化
    private function __wakeup()
    {

    }
}
```
