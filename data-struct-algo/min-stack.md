### 【时间】

2022年1月11日

[剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)



#### 【难度】

简单

#### 【题目】

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例：

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```





#### 【需要考虑的问题】

- 记录最小值，次小值
- 每次新的值入栈时，判断当前最小值栈的栈顶元素是否大于当前新值，大于则把新值入栈，反之，把栈顶元素再次入栈



#### 【解决过程】

```php
class MinStack {

    private $min_stack;
    private $stack;

    /**
     * initialize your data structure here.
     */
    function __construct() {
        $this->min_stack = [];
        $this->stack = [];
    }

    /**
     * @param Integer $x
     * @return NULL
     */
    function push($x) {
        $this->stack[] = $x;
        if (!$this->min_stack) {
            $this->min_stack[] = $x;
        } else {
            if ($this->min_stack[count($this->min_stack) - 1] > $x) {
                $this->min_stack[] = $x;
            } else {
                $this->min_stack[] = $this->min_stack[count($this->min_stack) - 1];
            }
        }
    }

    /**
     * @return NULL
     */
    function pop() {
        array_pop($this->stack);
        array_pop($this->min_stack);
    }

    /**
     * @return Integer
     */
    function top() {
        if ($this->stack) {
            return $this->stack[count($this->stack) - 1];
        }
        return -1;
    }

    /**
     * @return Integer
     */
    function min() {
        if ($this->min_stack) {
            return $this->min_stack[count($this->min_stack) - 1];
        }
        return -1;
    }
}
```

