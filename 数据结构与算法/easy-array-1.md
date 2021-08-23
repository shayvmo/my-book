### 删除排序数组中的重复项

2021年8月23日

LeetCode 地址：[删除排序数组中的重复项](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2gy9m/)



解析：双指针

**复杂度分析**

时间复杂度：O(n)，其中 n 是数组的长度。快指针和慢指针最多各移动 n 次。

空间复杂度：O(1)。只需要使用常数的额外空间。

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function removeDuplicates(&$nums) {
        $count = count($nums);
    	if ($count === 0) {
    		return 0;
    	}
    	$left = 0;
    	$right = 1;
    	while ($right < $count) {
    		if ($nums[$left] !== $nums[$right]) {
    			$nums[++$left] = $nums[$right];
    		}
    		$right++;
    	}
    	return ++$left;
    }
}
```

