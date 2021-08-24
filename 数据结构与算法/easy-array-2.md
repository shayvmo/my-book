

### 买卖股票的最佳时机II

2021年8月24日

LeetCode 地址：[买卖股票的最佳时机II](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2zsx1/)



解析：

【动态规划】

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



复杂度分析

时间复杂度：O(n)，其中 n 为数组的长度。一共有 2n 个状态，每次状态转移的时间复杂度为 O(1)，因此时间复杂度为 O(2n)=O(n)。

空间复杂度：O(n)。我们需要开辟 O(n) 空间存储动态规划中的所有状态。如果使用空间优化，空间复杂度可以优化至 O(1)。



【贪心】

由于股票的购买没有限制，因此整个问题等价于寻找 x 个**不相交**的区间 (l_i,r_i] 使得如下的等式最大化
$$
\quad \sum_{i=1}^{x}{a[r_i] - a[l_i]}
$$
其中  [l_i]表示在第 l_i 天买入，r_i表示在第 r_i天卖出。

贪心算法只能用于计算最大利润，**计算的过程并不是实际的交易过程**。



```php
class Solution {

    /**
     * @param Integer[] $prices
     * @return Integer
     */
    function maxProfit($prices) {
        // 贪心
        if (count($prices) === 0) {
            return 0;
        }
        $maxProfit = 0;
        for ($i=1; $i < count($prices); $i++) {
            $maxProfit += max(0, $prices[$i] - $prices[$i-1]);
        }
        return $maxProfit;
    }
}
```





复杂度分析

时间复杂度：O(n)，其中 n 为数组的长度。我们只需要遍历一次数组即可。

空间复杂度：O(1)。只需要常数空间存放若干变量。
