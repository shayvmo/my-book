## 存在重复元素



2021年8月26日

LeetCode 地址：[存在重复元素](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x248f5/)



方法一：使用内置函数

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function containsDuplicate($nums) {
		return count(array_unique($nums)) < count($nums);
    }
}
```



方法二：使用辅助数组

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function containsDuplicate($nums) {
		$temp = [];
        foreach($nums as $value) {
            if (isset($temp[$value])) {
                return true;
            }
            $temp[$value] = $value;
        }
        return false;
    }
}
```



方法三：排序，相邻2个元素相同则存在重复元素

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function containsDuplicate($nums) {
		sort($nums);
        for($i = 0; $i < count($nums) - 1 ; $i++ ) {
            if ($nums[$i] === $nums[$i+1]) {
                return true;
            }
        }
        return false;
    }
}
```

