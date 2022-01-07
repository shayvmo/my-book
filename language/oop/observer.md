# 观察者模式（Observer）

> 当对象的状态发生变化时，所有依赖于它的对象都得到通知并被自动更新。它使用的是低耦合的方式。

PHP 已经定义了2个接口用于快速实现观察者模式： SplObserver 和 SplSubject

```php
/**
 * User 实现观察者模式 (称为主体)，它维护一个观察者列表，
 * 当对象发生变化时，通知User
 */
class User implements \SplSubject
{
    private $email;
    
    private $observers;
    
    public function __construct()
    {
        $this->observers = new \SplObjectStorage();
    }

    public function attach(\SplObserver $observer)
    {
        $this->observers->attach($observer);
    }

    public function detach(\SplObserver $observer)
    {
        $this->observers->detach($observer);
    }

    public function changeEmail(string $email)
    {
        $this->email = $email;
        $this->notify();
    }

    public function notify()
    {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }      
    }
}


class UserObserver implements \SplObserver
{
    private $changeUsers = [];

    public function update(SplSubject $subject)
    {
         $this->changeUsers[] = clone $subject;
    }

    public function getChangedUsers()
    {
        return $this->changeUsers;
    }
}

class ObserverTest extends TestCase
{
    public function testChangeInUserLeadsToUserObserverBeingNotified()
    {
        $observer = new UserObserver();

        $user = new User();
        $user->attach($observer);

        $user->changeEmail('foo@bar.com');
        $this->assertCount(1, $observer->getChangedUsers());
    }
}
``` 

## 思考

观察者模式，首先有观察者和被观察者，当被观察者发生变化，通知观察者。

被观察者，需要实现注册观察者、移除观察者、通知观察者3个方法

观察者则需要实现通知接收方法，当收到被观察者通知时，执行操作。