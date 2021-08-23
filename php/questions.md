## 疑问汇总



**平常都使用的什么框架？Laravel 和 ThinkPHP 框架的区别？** Laravel 框架生命周期



**Laravel 常用到的功能有哪些？Laravel 依赖注入实现的原理是怎么样的？**

路由，模型，依赖注入，集合

依赖注入：反射



**Swoole 你用到了哪些功能？对协程这一块了解吗？**

http 服务器、websocket 服务器；



**能说说 PHP 的生命周期吗？传统的 php-fpm 模式和 swoole 有什么区别？**

模块初始化，请求初始化，执行阶段，请求关闭，模块关闭。

传统的 fpm 模式，fpm 处于 SAPI 层，PHP 底层在接收到 nginx 分发过来的请求，都会走一遍流程。

swoole 在环境初始化，模块初始化，请求初始化只执行一次，复用上一次的PHP初始环境。



**在项目中都是怎么用 hyperf 的？了解 hyperf 中的依赖注入实现原理吗？使用 hyperf 中的类是怎么实现的，是通过注解引入吗？**







**说说你在项目中使用到的 PHP 函数，任意说几个以及它的功能？**

- 时间类：date, strtotime，time

- 字符串类：strpos, str_replace, substr, strlen, trim

- 数组：array_column, array_walk, array_map, array_flip, sort, count, array_values, array_keys, explode, implode, array_merge,

- 数学类：round , floor, ceil, rand

- 判断变量： is_bool ,is_array 等

- 文件操作： file_get_contents, file_put_contents

- 其他：json_decode, json_encode, serialize, unserialize, base64_encode, base64_decode







**PHP 的垃圾回收机制是怎么样的？**

PHP 可以自动进行内存管理，清除不需要的对象。

PHP 使用了引用计数 (reference counting) GC 机制。

每个对象都内含一个引用计数器 refcount，每个 reference 连接到对象，计数器加 1。当 reference 离开生存空间或被设为 NULL，计数器减 1。当某个对象的引用计数器为零时，PHP 知道你将不再需要使用这个对象，释放其所占的内存空间。







**PHP5 的版本和 PHP7 之间有哪些区别？对 PHP8 了解吗，任意说说其中的新特性？**







**说说 php-fpm 与 NGINX 工作原理是怎么样的？**

nginx 借用 fastcgi 和 php-fpm 进行通信： TCP （跨服务器）、 Unix Socket （同服务器）

nginx 接收到 client 的请求， worker 进程根据 fastcgi 监听的地址，分发请求，php-fpm 监听接收到请求后，启用worker 进程处理请求，处理完成后，返回nginx ，nginx 将结果返回客户端