## JavaBean

在Java中，有很多`class`的定义都符合这样的规范：

- 若干`private`实例字段；
- 通过`public`方法来读写实例字段。



符合以下这种命名规范的类，称为JavaBean

```java
// 读方法:
public Type getXyz()
// 写方法:
public void setXyz(Type value)
```

