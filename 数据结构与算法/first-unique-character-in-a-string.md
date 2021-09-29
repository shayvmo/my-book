### 字符串中的第一个唯一字符



2021年9月29日

LeetCode地址： [字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)



#### 方法一：hash表计数出现频次

遍历2次字符串，第一次hash表记录各个字符出现的次数，第二次返回出现第一个一次的字符

```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function firstUniqChar($s) {
        $temp = [];
        $count = strlen($s);
        for ($i=0; $i < $count; $i++) {
            $temp[$s[$i]] = ($temp[$s[$i]] ?? 0 ) + 1;
        }

        for ($i=0; $i < $count; $i++) {
            if ($temp[$s[$i]] === 1) {
                return $i;
            }
        }
        return -1;
    }
}
```



复杂度分析：

- 时间复杂度：O(n)
- 空间复杂度：O(|E|) 取决于字符集



#### 方法二：hash表存储索引

hash表存储的键是字符，值是其对应的索引，这个索引包括实际索引值（仅出现一次）和 -1 （多次出现）



```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function firstUniqChar($s) {
        $temp = [];
        $count = strlen($s);
        for ($i=0; $i < $count; $i++) {
            $temp[$s[$i]] = isset($temp[$s[$i]]) ? -1 : $i;
        }

        foreach ($temp as $value) {
            if ($value !== -1) {
                return $value;
            }
        }
        return -1;
    }
}
```



复杂度分析：

- 时间复杂度：O(n)
- 空间复杂度：O(|E|) 取决于字符集



#### 方法三：队列

我们也可以借助队列找到第一个不重复的字符。队列具有「先进先出」的性质，因此很适合用来找出第一个满足某个条件的元素。

具体地，我们使用与方法二相同的哈希映射，并且使用一个额外的队列，按照顺序存储每一个字符以及它们第一次出现的位置。当我们对字符串进行遍历时，设当前遍历到的字符为 cc，如果 cc 不在哈希映射中，我们就将 cc 与它的索引作为一个二元组放入队尾，否则我们就需要检查队列中的元素是否都满足「只出现一次」的要求，即我们不断地根据哈希映射中存储的值（是否为 -1−1）选择弹出队首的元素，直到队首元素「真的」只出现了一次或者队列为空。

在遍历完成后，如果队列为空，说明没有不重复的字符，返回 -1−1，否则队首的元素即为第一个不重复的字符以及其索引的二元组。
