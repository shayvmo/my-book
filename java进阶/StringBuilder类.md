### StringBuilder 类

> 与 `String` 相似，`StringBuilder` 也是一个与字符串相关的类，Java 官方文档给 `StringBuilder` 的定义是：可变的字符序列

最近更新时间：2020年11月30日



---



字符串不可变性，当频繁操作字符串时，会在常量池产生很多无用的数据。

而 `StringBuilder` 与 `String` 不同，它具有**可变性**。相较 `String` 类不会产生大量无用数据，性能上会大大提高。

因此对于需要频繁操作字符串的场景，建议使用 `Stringbuilder` 类来代替 `String` 类。



`StringBuffer`

> 线程安全的可变字序列



#### 构造方法

`StringBuilder` 类提供了如下 4 个构造方法：

1. `StringBuilder()` 构造一个空字符串生成器，初始容量为 16 个字符；
2. `StringBuilder(int catpacity)` 构造一个空字符串生成器，初始容量由参数 `capacity` 指定；
3. `StringBuilder(CharSequence seq)` 构造一个字符串生成器，该生成器包含与指定的 `CharSequence` 相同的字符。；
4. `StringBuilder(String str)` 构造初始化为指定字符串内容的字符串生成器。

其中第 4 个构造方法最为常用，我们可以使用 `StringBuilder` 这样初始化一个内容为 `hello` 的字符串：

```java
StringBuilder str = new StringBuilder("hello");
```



#### 成员方法



#####  字符串连接

`  StringBuilder 的 StringBuilder append(String str)`

`append()` 方法返回的是一个`StringBuilder `类型，可以使用链式调用



##### 获取容量

> `int capacity()`
>
> 容量指定是可以存储的字符数（包含已写入字符），超过此数将进行自动分配。注意，容量与长度（length）不同，长度指的是已经写入字符的长度。



构造空字符串时，容量默认是16个字符。



##### 字符串替换

> 可以使用 `StringBuilder replace(int start, int end, String str)` 方法，来用指定字符串替换从索引位置 `start` 开始到 `end` 索引位置结束（不包含 `end`）的子串。



##### 字符串截取

> 可以使用 `StringBuilder substring(int start)` 方法来进行字符串截取
>
> 重载方法`StringBuilder substring(int start, int end)`截取



##### 字符串反转

> `StringBuildr reverse()`



