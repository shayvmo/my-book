# 二维数组中的查找

题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。



```
// 示例二维数组
1 2 8 9
2 4 9 12
4 7 10 13
6 8 11 15
```



**代码实现：**

1、PHP

```php
function findNum(array $array, int $target) {
    $rows = count($array);
    $cols = count($array[0]);
    $row = 0;
    $col = $cols -1;
    if ($rows === 0 || $target > $array[$row][$col]) {
        return false;
    }
    while($col >=0 && $row < $rows) {
        if ($target == $array[$row][$col]) {
            return true;
        }

        if ($target < $array[$row][$col]) {
            $col--;
        } else {
            $row++;
        }
    }
    return true;
}

$array = [
    [1,2,8,9],
    [2,4,9,12],
    [4,7,10,13],
    [6,8,11,15]
];
var_dump(findNum($array, 7));
```







2、Go

```go
func findNum(nums [][]int, target int) bool {
    rows := len(nums)
	cols := len(nums[0])
	if rows == 0 || target > nums[rows-1][cols-1] {
		return false
	}
	row := 0
	col := cols - 1
	for ;row < rows && col >= 0; {
		if nums[row][col] == target {
			return true
		}
		if target < nums[row][col] {
			col--
		} else {
			row++
		}
	}
	return false
}

func main() {
    nums := [][]int{{1,2,8,9}, {2,4,9,12}, {4,7,10,13}, {6,8,11,15}}
	fmt.Println(offer.FindNum(nums, 7))
}

```

