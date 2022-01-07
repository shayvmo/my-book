## 只出现一次的数字



2021年8月26日

LeetCode 地址：[只出现一次的数字](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x21ib6/)



常规解法

- 辅助 Hash 数组

- 集合

- array_count_values() （php内置函数）

  ```php
  class Solution {
  
      /**
       * @param Integer[] $nums
       * @return Integer
       */
      function singleNumber($nums) {
          $nums = array_count_values($nums);
          foreach ($nums as $key => $value) {
              if ($value === 1) {
                  return $key;
              }
          }
      }
  }
  ```

  



以上常规解法都会额外使用 O(n) 空间。



**异或位运算**

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function singleNumber($nums) {
		$single_number = 0;
        foreach($nums as $num) {
            $single_number ^= $num;
        }
        return $single_number;
    }
}
```



**注意：**异或位运算方式仅仅适用于 有1个元素出现一次，其他元素均出现 2 次的特定情况下。





