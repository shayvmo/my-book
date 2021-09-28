## 两个数组的交集-II



2021年9月28日

LeetCode 地址：[两个数组的交集 II](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2y0c2/)



给定两个数组，编写一个函数来计算它们的交集。



#### 方法一：hash表

1、遍历短数组借助hash表统计数字在短数组出现的次数

2、遍历长数组，如果hash数组存在当前元素，则减少一次hash数组元素出现次数，并将元素放进结果数组中。根据题目要求，返回较小的出现次数，当hash数组元素出现次数为0，说明短数组出现的次数比长数组少，这时不再把长数组元素放进结果数组。

注：先遍历短数组，后遍历长数组。

```php
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Integer[]
     */
    function intersect($nums1, $nums2) {
        if (count($nums1) > count($nums2)) {
            return $this->intersect($nums2, $nums1);
        }
        $temp = [];
        $result = [];
        foreach ($nums1 as $item) {
            $temp[$item] = ($temp[$item] ?? 0) + 1;
        }
        foreach ($nums2 as $item) {
            if (isset($temp[$item])) {
                if ($temp[$item] > 0) {
                    $result[] = $item;
                    $temp[$item]--;
                }
            }
        }
        return $result;
    }
}
```



#### 复杂度分析

- 时间复杂度：O(m+n)
- 空间复杂度：O(min(m+n))



#### 方法二：

