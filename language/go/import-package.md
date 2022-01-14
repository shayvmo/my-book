# Go语言中import导入包时：点. 、下划线_ 、别名的用法



转载于：[https://blog.csdn.net/qq_42346574/article/details/112260070](https://blog.csdn.net/qq_42346574/article/details/112260070)



刚接触Go的时候，在看别人的项目源码时，发现在import包的包名前面有一个下划线` _ `，产生疑问，于是搜索查阅资料。



以下示例代码在转载地址：

```go
import (
	v2 "github.com/YFJie96/wx-mall/controller/api/v2"
	_ "github.com/YFJie96/wx-mall/docs"
	. "fmt"
	"github.com/gin-gonic/gin"
	"github.com/swaggo/gin-swagger"
	"github.com/swaggo/gin-swagger/swaggerFiles"
)
```



相关资料说明：

- 别名` v2 `：

  相当于是导入包的一个别名，可以直接使用` v2. `调用包内接口或方法。

- 下划线` _ `：

  在导入路径前加入**下划线**表示**只执行该库的 init 函数**而不对其它导出对象进行真正地导入。因为 Go 语言的数据库驱动都会在 init 函数中注册自己，所以我们只需要进行上述操作即可；否则的话，**Go 语言的编译器会提示导入了包却没有使用的错误。**

- 点 `.` ：

  点相当于把导入包的函数，同级导入到当前包，可以直接使用包内函数名进行调用