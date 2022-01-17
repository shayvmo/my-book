# strings 和 strconv 包



1、前缀和后缀

```go
// 前缀
strings.HasPrefix(s, prefix string) bool

// 后缀
strings.HasSuffix(s, suffix string) bool
```



2、字符串包含关系

```go
strings.Contains(s, substr string) bool
```



3、判断子字符串和字符在父字符串中出现的位置（索引）

返回 -1 时，不存在

```go
// 首次出现的位置
strings.Index(s, str string) int

// 最后出现的位置
strings.LastIndex(s, str string) int
```



与字符串相关的类型转换都是通过` strconv ` 包来实现的

- `strconv.Itoa(i int) string` ：返回数字 i 所表示的字符串类型的十进制数
- `strconv.FormatFloat(f float64, fmt byte, prec int, bitsize int) string ` ：将 64 位浮点型的数字转换为字符串，其中 `fmt` 表示格式（其值可以是 `'b'`、`'e'`、`'f'` 或 `'g'`），`prec` 表示精度，`bitSize` 则使用 32 表示 float32，用 64 表示 float64



字符串转数字类型

- `strconv.Atoi(s string) (i int, err error)`： 将字符串转换为 int 型
- `strconv.ParseFloat(s string, bitSize int) (f float64, err error)`：将字符串转换为 float64 型