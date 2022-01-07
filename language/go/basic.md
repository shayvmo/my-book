**本章节内容来自《菜鸟教程》，并经过整理后记录**

导航
---

[TOC]

---
### 数据类型

- 布尔型
- 数字类型
- 字符串类型
- 派生类型
    - 指针类型
    - 数组类型
    - 结构化类型
    - Channel类型
    - 函数类型
    - 切片类型
    - 接口类型
    - Map类型

---

### 变量

- 全局变量允许声明而不使用，但是局部变量声明则必须使用

```
var identifier type

# 例如

var a int
a = 1

b := 2

fmt.Println(a, b)

```

```go
package main

var (
    x int
    y bool
)

func main() {
    var a, b int
    c := "shayvmo"
    fmt.Println(a, b, c, x, y)
}

// 输出
0 0 shayvmo 0 false
```

---

### 常量

```
const identifier [type] = value

// 显式类型定义
const a string = "abc"

// 隐式类型定义
const b = 4
```

#### iota

> iota 在 const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次(iota 可理解为 const 语句块中的行索引)

```
package main

func main() {
    const (
        a = iota
        b
        c
        d = "ha"
        e
        f = 100
        g
        h = iota
        i
    )
    fmt.Println(a, b, c, d, e, f, g, h, i)
}
```

---

### 位运算符

- `&` 按位与
- `|` 按位或
- `^` 按位异或
- `>>` 右移 右移n位，相当于是除以2的n次方
- `<<` 左移 左移n位，相当于是乘以2的n次方

---

### 条件语句

switch: 默认每个case都有break操作，只要匹配到了，则不再匹配。如果需要执行后面的case，可以使用 fallthrough 

```
switch a {
	case 1:
		fmt.Println("a匹配上了1")
		fallthrough
	case 2:
		fmt.Printf("a虽然匹配上了1，加上fallthrough也能执行下面的case")
	default:
		fmt.Println("default")
}
```

---

### 循环语句

```
for [init]; condition; [post] {}


# 例如

for i := 0; i < 10; i++ {}

i := 1;

for ; i < 10; {
    i += i * 2
}

```

---
### 函数

```
func function_name([params_list]) [return_type] {
    函数体
}
```

#### 函数的参数

- 值传递（默认）
- 引用传递

#### 函数用法

- 函数作为另一个函数的实参
- 闭包
- 方法

```
package main

import (
	"fmt"
	"strconv"
)

// 函数类型变量
type callBack func(int)

func main() {
	callBackTest(2, func(i int) {
		fmt.Println("回调的函数：" + strconv.Itoa(i))
	})
}

func callBackTest(x int, f callBack) {
	f(x)
}

```

---
### 变量作用域

- 全局
- 局部
- 形式参数

---
### 数组

```
# 声明数组
var varible_name [size] varible_type

# 长度为10的整型数组
var a [10] int 
```

初始化数组

```
# 初始化
var a = [...]int{1,2,3,4,5}

# 或
a := [...]int{2,24,42,3}

```

---
### 指针

```
# 声明格式
var var_name *var_type

# 执行int类型的指针 a1
var a1 *int

```

---
### 结构体

```
type struct_varible_type struct {
    member definition
    ...
    member definition
}

# 初始化
variable_name := structure_variable_type {value1, value2...valuen}
# 或
variable_name := structure_variable_type { key1: value1, key2: value2..., keyn: valuen}

```

例如

```
package main

type Book struct {
    title string
    author string
    book_id int
}


func main() {
    var book1 Book
    
	book1.title = "何以笙箫默"
	book1.author = "顾漫"
	book1.bookId = 123
}

```

#### 结构体指针

```
var struct_pointer *Book

var book1Pointer *Book
book1Pointer = &book1
fmt.Printf("%p\n", book1Pointer)

# 何以笙箫默
book1Pointer.title
```

---
### 切片

```
var identifier []type

func main() {
    arr := [...]int{1,2,3}

	var slice = make([]int, 5)
	slice1 := make([]int, 5)
	slice2 := []int {0,1,2,3,4,5,6,7}
	slice3 := arr[1:]
	
	fmt.Println(slice, slice1, slice2, slice3)
	
	slice2 = append(slice2, 8)
	slice4 := make([]int, len(slice2), cap(slice2) * 2)
	copy(slice4, slice2)
	printSlice(slice2)
	printSlice(slice4)
	
	fmt.Printf("slice2[1:4] = %v", slice2[1:4])
}

func printSlice(x []int) {
	fmt.Printf("len=%d cap=%d value=%v\n", len(x), cap(x), x)
}

```

#### append 和 copy

append 向切片添加元素

- 当 append 一个满的切片时，最大长度会自动扩容，并且扩容到当前cap的2倍

copy 复制原切片到新的切片（如果需要扩容时，需要先创建一个cap更大的切片，再把原切片复制过去）


---
### 范围Range

- 用于for循环中迭代数组（array），切片（slice），通道（channel），集合（map)的元素。
- 在数组和切片中返回索引和索引对应的值，在集合中返回key-value对

```
func testRange() {
   nums := [...]int{3,4,5,2}
   for _, v := range nums {
      fmt.Println(v)
   }

   maps := map[string]string{"a": "apple", "b": "banana"}
   for k, v := range maps {
      fmt.Printf("key: %s value: %s\n",k ,v)
   }

    // 第一个是字符的索引，第二个是字符的Unicode值
    for k, v := range "abcdefg" {
       fmt.Printf("%d -> %d", k, v)
    }

}
```
---

### Map集合

- 无序的键值对集合

#### 定义Map

```
var map_varible map[key_data_type]value_data_type

map_varible := make(map[key_data_type]value_data_type)

func testMap() {
	map1 := make(map[string]string)
	map1["a"] = "apple"
	for k, v := range map1 {
		fmt.Printf("%s -> %s\n", k, v)
	}
	// has 可以判断集合中是否含有这个元素
	value, has := map1["a"]
	fmt.Println(value, has)
}

```

delete() 函数
```
func delete(m map[Type]Type1, key Type)

delete(map1, "a")
```

---
### 接口

```
// 定义接口
type interface_name interface {
    method_name1 [return_type]
}

// 定义结构体
type struct_name struct {
    title string
}

// 实现接口方法
func (struct_name_varible struct_name) method_name1() [return_type] {
    
}

```

**实例**

```
package main

import "fmt"

type Phone interface {
	call()
	number() string
}

type NokiaPhone struct {

}

type Iphone struct {

}

func (nokiaPhone NokiaPhone) call()  {
	fmt.Println("Nokia")
}

func (iphone Iphone) call()  {
	fmt.Println("iphone")
}

func (nokiaPhone NokiaPhone) number() string  {
	return "nokia-phone-135478"
}

func (iphone Iphone) number() string  {
	return "iphone-13123"
}

func main() {
	testInterface()
}

func testInterface()  {
	var phone Phone
	phone = new(NokiaPhone)
	phone.call()
	fmt.Println(phone.number())

	phone = new(Iphone)
	phone.call()
	fmt.Println(phone.number())
}

```


---
### 错误处理

```
type error interface {
    Error() string
}


func testError(a int,b int) (int, error) {
	if b == 0 {
		return 0, errors.New("除数不能为0")
	}
	return a / b, nil
}

```

---
### 并发 goroutine

```
go 函数名( 参数列表 )
```

**通道channel** 

> 用于传递数据的一个数据结构。操作符 <- 指定通道方向，发送或接收。未指定方向则是双向通道

```

func main()  {
	s := []int{7, 2, 8, -9, 4, 0}
	c := make(chan int)
	go sum(s[:len(s)/2], c)
	go sum(s[len(s)/2:], c)
	x, y := <- c, <- c
	fmt.Println(x, y, x + y)
}

func sum(s []int, c chan int)  {
	sum := 0
	for _, v := range s {
		sum += v
	}

	c <- sum
}

```

**通道缓冲区**

- 第二个参数是缓冲区的大小

```
ch := make(chan int, 100)
```

**遍历通道与关闭通道**

range 遍历通道时，如果通道没有关闭，会一直阻塞等到通道，这时需要主动关闭通道

```
v, ok := <-ch
```
