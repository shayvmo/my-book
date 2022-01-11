### 【时间】
2022年1月9日

[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

#### 【难度】
简单

#### 【题目】
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和` deleteHead `，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead`操作返回 -1 )

#### 【需要考虑的问题】

- 注意栈的特点是后进先出
- 队列特点是先进先出



#### 【解决过程】

第一版: 指定一个唯一弹出操作的栈2，每次入栈，结合栈2和栈1，通过出入栈形成栈2，该版本频繁出入栈，会耗费更多的时间。


```
class CQueue {
    private $stack1;
    private $stack2;

    /**
     */
    function __construct() {
        $this->stack1 = [];
        $this->stack2 = [];
    }

    /**
     * @param Integer $value
     * @return NULL
     */
    function appendTail($value) {
        if (empty($this->stack1)) {
            $this->stack1[] = $value;
        } else {
            $len_1 = count($this->stack1);
            for($i = $len_1 - 1; $i >= 0; $i--) {
                $this->stack2[] = array_pop($this->stack1);
            }
            $this->stack1[] = $value;
            for($i = $len_1 - 1; $i >= 0; $i--) {
                $this->stack1[] = array_pop($this->stack2);
            }
        }
    }

    /**
     * @return Integer
     */
    function deleteHead() {
        if (empty($this->stack1)) {
            return -1;
        }
        return array_pop($this->stack1);
    }
}
```

第二版优化：栈1只管入栈，当需要出队时，栈1再通过出入栈移动到栈2，并弹出栈2元素

```
class CQueue {
    private $stack1;
    private $stack2;

    /**
     */
    function __construct() {
        $this->stack1 = [];
        $this->stack2 = [];
    }

    /**
     * @param Integer $value
     * @return NULL
     */
    function appendTail($value) {
        $this->stack1[] = $value;
    }

    /**
     * @return Integer
     */
    function deleteHead() {
        if (empty($this->stack1) && empty($this->stack2)) {
            return -1;
        }
        if (empty($this->stack2)) {
            while(!empty($this->stack1)) {
                $this->stack2[] = array_pop($this->stack1);
            }
        }
        return array_pop($this->stack2);
    }
}
```



Go 实现

```go
import "container/list"

type CQueue struct {
	stack1, stack2 *list.List
}


func Constructor() CQueue {
	return CQueue{
		stack1: list.New(),
		stack2: list.New(),
	}
}


func (this *CQueue) AppendTail(value int)  {
	this.stack1.PushBack(value)
}


func (this *CQueue) DeleteHead() int {
	if this.stack2.Len() == 0 {
		for this.stack1.Len() > 0 {
			this.stack2.PushBack(this.stack1.Remove(this.stack1.Back()))
		}
	}
	if this.stack2.Len() > 0 {
		e := this.stack2.Back()
		this.stack2.Remove(e)
		return e.Value.(int)// 断言是个int
	}
	return -1
}
```