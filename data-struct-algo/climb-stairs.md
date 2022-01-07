## 爬楼梯



2021年8月26日



LeetCode地址： [爬楼梯](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/xn854d/)



方法一：动态规划

```php
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function climbStairs($n) {
        $a = 0;
        $b = 0;
        $c = 1;
        for ($i = 1; $i <= $n; $i++) { 
            $a = $b;
            $b = $c;
            $c = $a + $b;
        }
        return $c;
    }
}
```



**复杂度分析**

时间复杂度：循环执行 n 次，每次花费常数的时间代价，故渐进时间复杂度为 O(n)。
空间复杂度：这里只用了常数个变量作为辅助空间，故渐进空间复杂度为 O(1)



方法二：矩阵快速幂



方法三：通项公式