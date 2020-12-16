### Optional 类

2020年12月15日



空指针异常（`NullPointerExceptions`）是 Java 最常见的异常之一，一直以来都困扰着 Java 程序员。一方面，程序员不得不在代码中写很多`null`的检查逻辑，让代码看起来非常臃肿；另一方面，由于其属于运行时异常，是非常难以预判的。



为了预防空指针异常，`Google`的`Guava`项目率先引入了`Optional`类，通过使用检查空值的方式来防止代码污染，受到`Guava`项目的启发，随后在`Java 8`中也引入了`Optional`类。



Optional 类位于`java.util`包下，是一个可以为 `null` 的**容器对象**，如果值存在则`isPresent()`方法会返回 `true` ，调用 `get()` 方法会返回该对象，可以有效避免空指针异常



#### 创建对象

- `Optional.of(T t)`：创建一个 Optional 对象，参数 `t` 必须非空；
- `Optional.empty()`：创建一个空的`Optional`实例；
- `Optional.ofNullable(T t)`：创建一个`Optional`对象，参数`t` 可以为 `null`



#### 常用方法

- `booean isPresent()`：判断是否包换对象；
- `void ifPresent(Consumer<? super T> consumer)`：如果有值，就执行 Consumer 接口的实现代码，并且该值会作为参数传递给它；
- `T get()`：如果调用对象包含值，返回该值，否则抛出异常；
- `T orElse(T other)`：如果有值则将其返回，否则返回指定的`other` 对象；
- `T orElseGet(Supplier<? extends T other>)`：如果有值则将其返回，否则返回由`Supplier`接口实现提供的对象；
- `T orElseThrow(Supplier<? extends X> exceptionSupplier)`：如果有值则将其返回，否则抛出由`Supplier`接口实现提供的异常。