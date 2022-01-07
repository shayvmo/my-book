# 插入排序

>每一趟将一个待排序的记录，按其关键字的大小插入到已经排好序的一组记录的适当位置上，直到所有待排序记录全部插入为止



- 直接插入排序
- 折半插入排序
- 希尔排序





### 直接插入排序



代码实现

```php
function insert_sort(&$arr) {
    $count = count($arr);
    for ($i = 1; $i < $count; $i++) {
        if ($arr[$i-1] > $arr[$i]) {
            $temp = $arr[$i];
            for ($j=$i-1; $arr[$j] > $temp; $j--) {
                $arr[$j+1] = $arr[$j];
            }
            $arr[$j+1] = $temp;
        }
    }
}
```



在平均情况下，直接插入排序关键字的比较次数和记录移动次数均约为 
$$
n^2 / 4
$$


时间复杂度为
$$
O(n^2)
$$
空间复杂度为
$$
O(1)
$$






【算法特点】

稳定排序

可用于链式结构



### 折半插入排序



代码实现

```php
function binary_insert_sort(&$arr) {
    $count = count($arr);
    for ($i = 1; $i < $count; $i++) {
        $temp = $arr[$i];
        $low = 0;
        $high = $i-1;
        while ($low <= $high) {
            $m = floor(($low + $high) / 2);
            if ( $temp < $arr[$m] ) {
                $high = $m - 1;
            } else {
                $low = $m + 1;
            }
        }
        for ($j=$i-1; $j >= $high; $j--) {
            $arr[$j+1] = $arr[$j];
        }
        $arr[$high+1] = $temp;
    }
}
```



时间复杂度、空间复杂度和直接插入排序一样，只是减少了比对次数



【稳定性】

稳定排序

折半查找只能用于顺序结构，不能用于链式结构

适合初始记录无序，N 较大

