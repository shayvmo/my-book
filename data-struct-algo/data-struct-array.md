# 线性表结构之数组

> 数组是由类型相同的数据元素构成的有序集合。

> 由类型相同的元素构成的有序集合，并且使用一块连续内存存储。

- 随机访问
- 容量有限

假设数组的长度是n，

访问数组： `O(1)`

插入：`O(n)` (最坏情况下)

删除：`O(n)` (最坏情况下)

## 数组的基本操作

- 初始化数组

- 销毁数组

- 数组赋值

- 取数组的某个元素

- 复制一个数组

- 打印数组的元素

## 数组的存储

- 一维数组

按照顺序存储，物理地址和逻辑地址都是连续的

- 多维数组

(1) 行优先顺序

存储时，先按行从小到大的顺序存储，在每一行中按列号从小到大存储。

(2) 列优先顺序

存储时，先按列从小到大的顺序存储，在每一列中按行号从小到大存储。

```php
$arr = [
    [1, 3, 5], 
    [2, 4, 6],
    [3, 8, 9],
    [4, 7, 10]
];

$arr_new = [];

// 行优先顺序
for ($i = 0; $i < 4; $i++) {
    for ($j = 0; $j < 3; $j++) {
        $arr_new[$i * 3 + $j] = $arr[$i][$j];
    }
}
var_dump(implode('-', $arr_new));// 1-3-5-2-4-6-3-8-9-4-7-10

//$arr_new = [];
// 列优先顺序
for ($i = 0; $i < 4; $i++) {
    for ($j = 0; $j < 3; $j++) {
        $arr_new[$j* 4 + $i] = $arr[$i][$j];
    }
}
var_dump(implode('-', $arr_new));// 1-2-3-4-3-4-8-7-5-6-9-10

```

## 矩阵的存储



- 对称矩阵
- 三角矩阵
- 对角矩阵