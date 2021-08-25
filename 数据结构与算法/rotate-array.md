## 旋转数组

2021年8月25日

LeetCode 地址：[旋转数组](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2skh7/)



题解：[LeetCode官方题解](https://leetcode-cn.com/problems/rotate-array/solution/xuan-zhuan-shu-zu-by-leetcode-solution-nipk/)



方法一：取模的方式，使用额外的数组

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return NULL
     */
    function rotate(&$nums, $k) {
        if (count($nums) <= 1) {
            return $nums;
        }
        $newNums = [];
        for ($i=0; $i < count($nums); $i++) {
            $key = ($i + $k)%count($nums);
            $newNums[$key] = $nums[$i];
        }
        ksort($newNums);
        $nums = $newNums;
        return $nums;
    }
}
```

**复杂度分析**

- 时间复杂度： O(n)，其中 n为数组的长度。一次遍历，取决于数组的长度。
- 空间复杂度： O(n)。使用额外的数组保存，空间取决于原数组长度。



方法二：环状替换





方法三：数组翻转

1、翻转全部元素

2、翻转[0, k mod n-1 ] 区间元素

3、翻转[k mod n , n -1 ] 区间元素

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return NULL
     */
    function rotate(&$nums, $k) {
        if (count($nums) <= 1) {
            return $nums;
        }
        $reverse = function(&$arr, $start, $end) {
            $count = $end - $start + 1;
            $mid = ($end + $start) / 2;
            for ($i=$start; $i < $mid; $i++) {
                [$arr[$i], $arr[2 * $mid - $i]] = [$arr[2 * $mid - $i], $arr[$i]];
            }
        };
        $k %= count($nums);
        $reverse($nums, 0, count($nums) - 1);
        $reverse($nums, 0, $k - 1);
        $reverse($nums, $k, count($nums) - 1);
        return $nums;
    }
}
```

**复杂度分析**

- 时间复杂度：O(n)，其中 n为数组的长度。每个元素被翻转两次，一共 n个元素，因此总时间复杂度为 O(2n)=O(n)。

- 空间复杂度：O(1)。