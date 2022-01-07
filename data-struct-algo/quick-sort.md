# 快速排序

> 选择一个基准数，通过一趟排序将要排序的数据分割成独立的两部分；其中一部分的所有数据都比另外一部分的所有数据都要小。然后，再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。



:memo: 2021年7月29日11:14



:exclamation: 选择一个基准数，小值在左，大值在右，递归左子数列和右子数列



核心思想是分治法，分而治之



## 单边扫描

> 我们随意抽取一个数作为基准值，同时设定一个标记 mark 代表左边序列最右侧的下标位置，当然初始为 0 ，接下来遍历数组，如果元素大于基准值，无操作，继续遍历，如果元素小于基准值，则把 mark + 1 ，再将 mark 所在位置的元素和遍历到的元素交换位置，mark 这个位置存储的是比基准值小的数据，当遍历结束后，将基准值与 mark 所在元素交换位置即可。



遍历数列后，mark 下标所在元素为数列中，小于基准值的最右侧元素，此时mark下标左侧数列包含基准值，交换基准值和mark位置元素后，基准值位置左侧的所有元素都是小于基准值，右侧所有元素都是大于基准值



### 代码实现

```php
function quick_sort_1(array &$arr, $start_index, $end_index)
{
    if ($start_index >= $end_index) {
        return;
    }
    $mark = $start_index;// mark 初始化为起始下标
    $standard = $arr[$start_index];// 基准值
    // 从基准值下一位开始遍历数列
    for ($i = $start_index + 1; $i <= $end_index; $i++) {
        if ($arr[$i] < $standard) {// 小于基准值的元素，mark + 1, 并交换mark位置和i位置元素
            $mark++;
            [$arr[$i], $arr[$mark]] = [$arr[$mark], $arr[$i]];// 不借助变量交换两个变量的值
            
            //$temp = $arr[$mark];
            //$arr[$mark] = $arr[$i];
            //$arr[$i] = $temp;
        }
    }
    $arr[$start_index] = $arr[$mark];
    $arr[$mark] = $standard;
    quick_sort_1($arr, $start_index, $mark - 1);
    quick_sort_1($arr, $mark + 1, $end_index);
}

$arr = [6, 2, 3, 5, 1, 8, 7, 4, 9, 2];
quick_sort_1($arr, 0, count($arr) - 1);
var_dump($arr);
```







## 双边扫描

> 我们随意抽取一个数作为基准值，然后从数组左右两边进行扫描，先从左往右找到一个大于基准值的元素，将下标指针记录下来，然后转到从右往左扫描，找到一个小于基准值的元素，交换这两个元素的位置，重复步骤，直到左右两个指针相遇，再将基准值与左侧最右边的元素交换。







### 代码实现

```php
// 双边扫描
function quick_sort(array &$arr, int $start_index, int $end_index)
{
    if ($end_index > $start_index) {
        $left = $start_index;
        $right = $end_index + 1;
        $standard = $arr[$start_index];// 切分标准值
        while (true) {
            // 从左往后查找大的数据
            while ($arr[++$left] < $standard) {
                if ($left === $end_index) {
                    break;
                }
            }
            // 从右往左查找小的数据
            while ($arr[--$right] > $standard) {
                if ($right === $start_index) {
                    break;
                }
            }
            // 下标指针相遇，停止循环，切分完成
            if ($left >= $right) {
                break;
            }
            // 交换大值和小值元素
            [$arr[$left], $arr[$right]] = [$arr[$right], $arr[$left]];
        }
        // 一轮切分完成，交换左侧小值最右侧元素和标准值
        [$arr[$start_index], $arr[$right]] = [$arr[$right], $arr[$start_index]];
        // 分治递归
        quick_sort($arr, $start_index, $right - 1);
        quick_sort($arr, $right + 1, $end_index);
    }
}


$arr = [6, 2, 3, 5, 1, 8, 7, 4, 9, 2];
quick_sort_1($arr, 0, count($arr) - 1);
var_dump($arr);
```





## 拓展

- 当一个数列元素个数比较少时，使用插入排序，效率会更高。

  > 基于上述实现的算法，加上以下判断

```php
if ($end_index <= $start_index + N ) {
    insert_sort($arr, $start_index, $end_index);
}
```



转换参数值 N 的最佳值和系统相关的，但是在 5 ~ 15 之间的任意值在大多数情况下都能令人满意的。





- 如果数组有很多重复的元素时，可选择熵最优的排序。一个简单的想法就是把数组切分成3个部分，分别对应小于、等于、大于的数组元素。

