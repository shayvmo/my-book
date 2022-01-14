# 选择排序

> 遍历数组，每次选出最大或最小的元素，直至数组有序。



### 代码实现

```php
$array = [4, 5, 2, 1, 3, 9, 7, 8, 6];

function select_sort($array) {
    $count = count($array);
    if ($count === 0) {
        return $array;
    }
    for($i = 0; $i < $count; $i++) {
        $temp_min = $array[$i];
        $temp_min_index = $i;
        for ($j = $i + 1; $j < $count; $j++) {
            if ($array[$j] < $temp_min) {
                $temp_min = $array[$j];
                $temp_min_index = $j;
            }
        }
        [$array[$i], $array[$temp_min_index]] = [$array[$temp_min_index], $array[$i]];
    }
    return $array;
}
```

