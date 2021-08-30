## 反转字符串



2021年8月30日

LeetCode 地址：[反转字符串](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/xnhbqj/)



```php
class Solution {

    /**
     * @param String[] $s
     * @return NULL
     */
    function reverseString(&$s) {
        $end = count($s) - 1;
        if ($end <= 0) {
            return $s;
        }
        $start = 0;
        while ($start != $end) {
            [$s[$start], $s[$end]] = [$s[$end], $s[$start]];
            $start++;
            $end--;
            if ($start >= $end) {
                break;
            }
        }
        return $s;
    }
}
```

