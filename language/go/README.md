# Go


> Go 语言入门


- [Goland debug 遇到低版本的delve](delve-old-version.md)
- [数据类型](data-type.md)
- [基础入门](basic.md)
- [Go语言中import导入包时：点. 、下划线_ 、别名的用法](import-package.md)
- [strings 和 strconv 包](strings-strconv.md)



### 数据类型

#### 切片

> 切片源于数组，当从数组切出部分数据成切片时，会存在数据共享问题



切片数据结构

```go
type slice struct {
    array unsafe.Pointer //指向存放数据的数组指针
    len   int            //长度有多大
    cap   int            //容量有多大
}
```



以下例子会出现数据共享问题：

```go
slice1 := []int{1,2,3,4,5}
slice2 := slice1[1:3]
slice2[1] = 6
fmt.Println("slice1:", slice1) // slice1: [1 2 6 4 5]
fmt.Println("slice2:", slice2) // slice2: [2 6]
```

