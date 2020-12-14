### Java 日期和时间



最近更新时间：2020年12月14日



#### Date 类的使用

> `java.util.Date` 类日期表示特定的时间瞬间，精度为毫秒



##### 构造方法

- `Date()`：创建一个对应当前时间的日期对象；
- `Date(long date)`：创建指定毫秒数的日期对象



##### 常用方法

- `String toString()`：将此日期对象转换为以下形式的字符串：星期 月 日 时:分:秒 时区 年；
- `long getTime()`：返回此日期对象表示的自1970年1月1日00:00:00 GMT以来的毫秒数；
- `void setTime()`：将此日期对象设置为表示1970年1月1日00:00:00 GMT之后的时间点（毫秒）





#### Calendar 类的使用

> Calendar类是一个抽象类，它提供了一些方法，用于在特定的时间瞬间与一组日历字段（如年、月、月、日、小时等）之间进行转换，以及用于处理日历字段（如获取下一周的日期）。



获取实例对象

- 使用`Calendar.getInstance()`方法（更常用）；
- 调用它的子类的`GregorianCalendar`的构造方法。



##### 常用方法

- `static Calendar getInstance()`：使用默认时区和区域设置获取日历；
- `int get(int field)`：返回给定日历字段的值；
- `void set(int field, int value)`：将给定的日历字段设置为给定值。（此外，`set()`还有很多重载方法）





#### Java8 后新的日期和时间 API

`LocalTime`（本地日期）、`LocalDate`（本地时间）、`LocalDateTime`（本地日期时间）、`ZonedDateTime`（带时区的日期时间）和`Duration`（时间间隔）类

```java
LocalDate localDate = LocalDate.now();
LocalTime localTime = LocalTime.now();
LocalDateTime localDateTime = LocalDateTime.now();
System.out.println(localDate);
System.out.println(localTime);
System.out.println(localDateTime);
```

































