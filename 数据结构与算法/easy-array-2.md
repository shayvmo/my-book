

### 买卖股票的最佳时机II

2021年8月23日

LeetCode 地址：[买卖股票的最佳时机II](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2zsx1/)



解析：

考虑到「不能同时参与多笔交易」，因此每天交易结束后只可能存在手里有一支股票或者没有股票的状态。

dp0 表示交易后手里没有股票的最大利润

dp1 表示交易后手里有股票的最大利润

直至最后一个交易日手里没有股票的利润一定最大，所以最终返回的是 dp0 

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
        $count = count($prices);
        $dp0 = 0;
        $dp1 = -$prices[0];
        for ($i=1; $i < $count; $i++) { 
            $tempDp0 = max($dp0, $dp1 + $prices[$i]);// 比较前1天没有股票，和今天卖出股票的最大收益
            $tempDp1 = max($dp1, $dp0 - $prices[$i]);// 比较前1天有股票，和今天买入股票的最大收益
            $dp0 = $tempDp0;
            $dp1 = $tempDp1;
        }
        return $dp0;
    }
}
```

