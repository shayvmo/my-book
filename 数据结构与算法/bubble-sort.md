# 冒泡排序 Bubble-sort

> 简单的排序算法，遍历多次需要排序的数列。每次遍历时，它都会从前往后依次的比较相邻两个数的大小；如果前者比后者大，则交换它们的位置。这样，一次遍历之后，最大的元素就在数列的末尾！ 采用相同的方法再次遍历时，第二大的元素就被排列在最大元素之前。重复此操作，直到整个数列都有序为止！



:memo: 2021年7月27日17:57



## 代码实现



```php
function bubble_sort(array $arr)
{
    if (count($arr) <= 1) {
        return $arr;
    }
    for ($i = 0; $i < count($arr) - 1; $i++) {
        $sort = false;
        for ($j = 0; $j < count($arr) - $i - 1; $j++) {
            if ($arr[$j] > $arr[$j + 1]) {
                $temp = $arr[$j + 1];
                $arr[$j + 1] = $arr[$j];
                $arr[$j] = $temp;
                $sort = true;
            }
        }
        if (!$sort) {
            break;
        }
    }
    return $arr;
}

$arr = [4, 5, 2, 1, 3, 9, 7, 8, 6];
var_dump(bubble_sort($arr));
```



` $sort ` 表示假设在第n次遍历的时候，后面的元素没有发生位置交换，说明已经是有序的，所以停止遍历。





## 稳定性

稳定算法，如果数列中 ` a ` 等于` b `，排序前，`a `在` b `的前面，那么排序后，` a `也在` b `的前面。