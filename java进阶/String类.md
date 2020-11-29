### String 类

> 引用数据类型

最近更新时间：2020年11月29日

#### 【String 对象的创建】

- 创建字符串方式

  ```java
  String str1 = "Hello, world";
  ```



- 对象实例化	

  ```java
  String str1 = new String("Hello, world")；
  ```



- 无参构造，创建一个空字符串

  ```java
  String str3 = new String();
  ```





#### 【获取字符串长度】

- `length()` 获取长度



#### 【字符串查找】

- 获取指定位置的字符

  - `char charAt(int index)`

  - ```java
    String str = "string1";
    System.out.println(str.charAt(2)); // 打印 r
    ```

    

- 查找字符串的位置

  - `indexOf()` 获取字符或子串在字符串中第一次出现的位置。
  - `lastIndexOf()`  获取字符或子串在字符串中最后一次出现的位置。



> 这里的**子串**指的就是字符串中的连续字符组成的子序列。例如，字符串 `Hello` 就是字符串 `Hello Java` 的子串。



#### 【字符串截取】

字符串的截取也称为**获取子串**，在实际开发中经常用到，可以使用 `substring()` 方法来获取子串，String 类中有两个重载的实例方法：

- `String substring(int beginIndex)` 获取从 `beginIndex` 位置开始到结束的子串。
- `String substring(int beginIndex, int endIndex)` 获取从 `beginIndex` 位置开始到 `endIndex` 位置的子串（不包含 `endIndex` 位置字符）。



```java
public class StringMethod3 {
    public static void main(String[] args) {
        String str = "I love Java";
        String substring = str.substring(2);
        String substring1 = str.substring(2, 6);
        System.out.println("从索引位置2到结束的子串为：" + substring);
        System.out.println("从索引位置2到索引位置6的子串为：" + substring1);
    }
}
// 从索引位置2到结束的子串为：love Java
// 从索引位置2到索引位置6的子串为：love
```

【！！！】要特别注意，方法签名上有两个参数的 `substring(int beginIndex, int endIndex)` 方法，截取的子串不包含 `endIndex` 位置的字符。



#### 【字符串切割】

- 切割成字串数组

  - `String[] split(String regex)` 方法可将字符串切割为子串，其参数 `regex` 是一个正则表达式分隔符，返回字符串数组

    

- 切割成 byte 数组

  - 使用 `getBytes()` 方法将字符串转换为 `byte` 数组



#### 【大小写转换】

字符串的大小写转换有两个方法：

- `toLowerCase()` 将字符串转换为小写
- `toUpperCase()` 将字符串转换为大写



#### 【字符串比较】

`String` 类提供了 `boolean equals(Object object)` 方法来比较字符串内容是否相同，返回一个布尔类型的结果。

需要特别注意的是，在比较字符串内容是否相同时，必须使用 `equals()` 方法而不能使用 `==` 运算符。



