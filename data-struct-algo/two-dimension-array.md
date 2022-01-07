# 二维数组中的查找

题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。



leetcode地址：[https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)





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
function findNumberIn2DArray($matrix, $target) {
    $rows = count($matrix);
    if ($rows === 0) {
        return false;
    } 
    $cols = count($matrix[0]);
    if ($cols === 0) {
        return false;
    }
    if ($target > $matrix[$rows - 1][$cols - 1]) {
        return false;
    }
    $row = 0;
    $col = $cols -1;
    while($col >=0 && $row < $rows) {
        if ($target === $matrix[$row][$col]) {
            return true;
        }

        if ($target < $matrix[$row][$col]) {
            $col--;
        } else {
            $row++;
        }
    }
    return false;
}

$array = [
    [1,2,8,9],
    [2,4,9,12],
    [4,7,10,13],
    [6,8,11,15]
];
var_dump(findNumberIn2DArray($array, 7));
```







2、Go

```go
func findNumberIn2DArray(matrix [][]int, target int) bool {
    rows := len(matrix)
	if rows == 0 {
		return false
	}
	cols := len(matrix[0])
	if cols == 0 {
		return false
	}
	if target > matrix[rows-1][cols-1] {
		return false
	}
	row := 0
	col := cols - 1
	for ;row < rows && col >= 0; {
		if matrix[row][col] == target {
			return true
		}
		if target < matrix[row][col] {
			col--
		} else {
			row++
		}
	}
	return false
}

func main() {
    nums := [][]int{{1,2,8,9}, {2,4,9,12}, {4,7,10,13}, {6,8,11,15}}
	fmt.Println(findNumberIn2DArray(nums, 7))
}

```

