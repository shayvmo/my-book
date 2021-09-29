### 两数之和



2021年9月29日

LeetCode地址：[https://leetcode-cn.com/problems/two-sum/](https://leetcode-cn.com/problems/two-sum/)





方法一：暴力枚举

- 时间复杂度：O(N^2)，其中 N 是数组中的元素数量。最坏情况下数组中任意两个数都要被匹配一次。
- 空间复杂度：O(1)。



方法二：哈希表

- 时间复杂度：O(N)
- 空间复杂度： O(N)

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        $temp = [];
        foreach ($nums as $key => $value) {
            if (isset($temp[$target-$value])) {
                return [$temp[$target-$value], $key];
            }
            $temp[$value] = $key;
        }
        return [];
    }
}
```

