

### 买卖股票的最佳时机

2021年8月23日

LeetCode 地址：[买卖股票的最佳时机](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/xn8fsh/)



解析：

**复杂度分析**

- 时间复杂度：O(n)，只需要遍历一次。
- 空间复杂度：O(1)，只使用了常数个变量。

```php
class Solution {

    /**
     * @param Integer[] $prices
     * @return Integer
     */
    function maxProfit($prices) {
		if (count($prices) === 0) {
    		return 0;
    	}
        $minPrice = $prices[0];
        $maxProfit = 0;
        foreach ($prices as $value) {
            $value < $minPrice && $minPrice = $value;
            $value - $minPrice > $maxProfit && $maxProfit = $value - $minPrice;
        }
        return $maxProfit;
    }
}
```
