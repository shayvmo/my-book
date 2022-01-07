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



#### 方法二：排序 + 双指针

首先对两个数组进行排序，然后使用两个指针遍历两个数组。

初始时，两个指针分别指向两个数组的头部。每次比较两个指针指向的两个数组中的数字，如果两个数字不相等，则将指向较小数字的指针右移一位，如果两个数字相等，将该数字添加到答案，并将两个指针都右移一位。当至少有一个指针超出数组范围时，遍历结束。



```php
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Integer[]
     */
    function intersect($nums1, $nums2) {
        sort($nums1);
        sort($nums2);
        $count1 = count($nums1);
        $count2 = count($nums2);
        $result = [];
        $i = 0;
        $j = 0;

        while ($i < $count1 && $j < $count2) {
            if ($nums1[$i] === $nums2[$j]) {
                $result[] = $nums1[$i];
                $i++;
                $j++;
            } else {
                $nums1[$i] < $nums2[$j] && $i++;
                $nums1[$i] > $nums2[$j] && $j++;
            }
        }

        return $result;
    }
}
```



#### 复杂度分析

- 时间复杂度：O(m log m +  n log n)，其中 m 和 n 分别是两个数组的长度。对两个数组进行排序的时间复杂度是 O(mlogm+nlogn)，遍历两个数组的时间复杂度是 O(m+n)，因此总时间复杂度是 O(mlogm+nlogn)。

- 空间复杂度：O(min(m,n))，其中 m 和 n 分别是两个数组的长度。为返回值创建一个数组 intersection，其长度为较短的数组的长度。不过在 C++ 中，我们可以直接创建一个 vector，不需要把答案临时存放在一个额外的数组中，所以这种实现的空间复杂度为 O(1)。



### 进阶

- 给定的数组都有序，采用双指针的方式