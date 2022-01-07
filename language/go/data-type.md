# 数据类型

最后更新于：2021-3-23 23:32

## 变量、作用域、常量和枚举

### 变量

变量声明

```go
var i int
var (
    v1 int                // 整型，默认值：0
    v2 string             // 字符串，默认空字符串
    v3 bool               // 布尔型，默认false
    v4 [2]int             // 数组，数组元素为整型 默认：[0,0]
    v5 struct {           // 结构体，成员变量f的类型是float64，默认 {0}
        f float64
    }
    v6 *int               // 指针，指向整型,默认 nil
    v7 map[string]int     // map（字典）， key是字符串类型，value是整型，默认map[]
    v8 func(a int)int     // 函数，参数整型，返回值整型，默认nil
)

```

命名规则

小驼峰法：`userName`，如果是全局变量希望能够被外部使用，则使用大驼峰法 `UserName`

变量初始化

```go
var v1 int = 10
var v2 = 10
v3 := 10   // 左侧的变量应该未声明过，否则编译错误
```

变量赋值和多重赋值
```go
# 初始化后，赋值
var v int
v = 123

# 多重赋值
i, j = j, i

```

匿名变量
```go
func getName() (userName, nickName string) {
    return "农夫山泉", "哇哈哈"
}
```

常量的作用域
> 大写字母开头包外可访问，小写字母开头只能包内访问



示例程序：
```go
package main

import "fmt"

// 常量定义
const (
	Pi float64 = 3.1415926535897
)

// a=3 b=4 c="C"
const a, b, c = 3, 4, "C"

// 报错，右侧值无法确定
//const num = GetNumber()

// 预定义常量
// true
// false
// iota： 可被编译器修改的常量，在每一个 const 关键字出现时被重置为 0，
// 然后在下一个 const 出现之前，每出现一次 iota，其所代表的数字会自动增 1

const (
	a = itoa // 0
	b = itoa // 1
	c = itoa // 2
)

// 以上可以简写成
const (
	a = itoa
	b
	c
)

const a1 = itoa // 0
const a2 = itoa // 0

// 枚举
const (
	Sunday = iota
	Monday
	Tuesday
	Wednesday
	Thursday
	Friday
	Saturday
	numberOfDays
)

func main()  {
	// 变量声明
	var (
		v1 int
		nickName string
	)

	// 变量初始化
	v2 := 98

	// 变量赋值
	v1 = 100

	fmt.Println(v1, v2)

	// 多重赋值
	v1, v2 = v2, v1
	fmt.Println(v1, v2)

	// 匿名变量 _
	_, nickName = GetName()
	fmt.Println(nickName)
}

func GetName() (userName, nickName string)  {
	return "Go", "Golang"
}

func GetNumber() int {
	return 10
}
```
