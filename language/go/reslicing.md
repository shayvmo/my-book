## 切片重组reslice

> 改变切片长度的过程称之为切片重组 **reslicing**，做法如下：`slice1 = slice1[0:end]`，其中 end 是新的末尾索引（即长度）。



```go
ar := [...]int{0,1,2,3,4,5,6,7,8,9}
var a = ar[3:3]
var b = ar[3:4]
// [] 7 0
fmt.Println(a, cap(a), len(a))
// [3] 7 1
fmt.Println(b, cap(b), len(b))
```

