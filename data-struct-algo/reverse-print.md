### 【时间】
2022年1月11日

[剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

#### 【难度】
简单

#### 【题目】

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。




#### 【需要考虑的问题】

- 边界



#### 【解决过程】



第一版：数组头插法

```php
class Solution {

    /**
     * @param ListNode $head
     * @return Integer[]
     */
    function reversePrint($head) {
        $return = [];
        $now_node = $head;
        while (true) {
            array_unshift($return, $now_node->val);
            if (is_null($now_node->next)) {
                break;
            }
            $now_node = $now_node->next;
        }
        return $return;
    }
}
```



第二版：数组尾插法，再反转数组

相比头插法，减少了元素的移动次数，会节省更多时间

```php
class Solution {

    /**
     * @param ListNode $head
     * @return Integer[]
     */
    function reversePrint($head) {
        $return = [];
        $now_node = $head;
        while (true) {
            $return[] = $now_node->val;
            if (is_null($now_node->next)) {
                break;
            }
            $now_node = $now_node->next;
        }
        return array_reverse($return);
    }
}
```

