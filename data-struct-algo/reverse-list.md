### 【时间】

2022年1月14日

#### [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

#### 【难度】

简单

#### 【题目】

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。




#### 【需要考虑的问题】

- 边界



#### 【解决过程】



1、递归

```php
function reverseList($head) {
    if (is_null($head) || is_null($head->next)) {
        return $head;
    }
    $next_node = $head->next;
    $first_node = $this->reverseList($next_node);// 找出尾结点，作为头结点返回递归
    //-- 相邻结点位置互换，递归返回上层
    $next_node->next = $head;
    $head->next = null;
    return $first_node;
}
```





2、迭代

```php
function reverseList($head) {
    if (is_null($head) || is_null($head->next)) {
        return $head;
    }
    $node = null;
    // 新链表头插法
    while(!is_null($head)) {
        $temp_node = $node;
        $node = new ListNode($head->val);
        $node->next = $temp_node;
        $head = $head->next;
    }
    return $node;
}
```

