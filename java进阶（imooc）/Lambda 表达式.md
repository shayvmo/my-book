### Lambda 表达式



最近更新于：2020年12月15日



#### 基础语法

Lambda 表达式由三个部分组成：

- **一个括号内用逗号分隔的形式参数列表**：实际上就是接口里面抽象方法的参数；

- **一个箭头符号**：->，这个箭头我们又称为 Lambda 操作符或箭头操作符；

- **方法体**：可以是表达式和代码块，是重写的方法的方法体。语法如下

  - 方法体为表达式，该表达式的值作为返回值返回

    ```java
    (parameters) -> expression
    ```

    

  - 方法体为代码块，必须用 {} 来包裹起来，且需要一个 return 返回值，但若函数式接口里面方法返回值是 void，则无需返回值

    ```java
    (parameters) -> {
        statement1; 
        statement2;
    }
    ```



#### 使用实例



1、无参数无返回值

无参数无返回值，指的是接口实现类重写的方法是无参数无返回值的

```java
public class LambdaDemo2 {

    public static void main(String[] args) {
        // 通过匿名内部类实例实例化一个 Runnable 接口的实现类
        Runnable runnable1 = new Runnable() {
            @Override
            public void run() {  // 方法无形参列表，也无返回值
                System.out.println("Hello, 匿名内部类");
            }
        };
        // 执行匿名内部类的 run() 方法
        runnable1.run();

        // 无参数无返回值，通过 lambda 表达式来实例化 Runnable 接口的实现类
        Runnable runnable2 = () -> System.out.println("Hello, Lambda");
        // 执行通过 lambda 表达式实例化的对象下的 run() 方法
        runnable2.run();
    }

}
```



2、单参数无返回值

单参数无返回值，指的是接口实现类重写的方法是单个参数，返回值为 `void` 

```java
import java.util.function.Consumer;

public class LambdaDemo3 {

    public static void main(String[] args) {

        // 单参数无返回值
        Consumer<String> consumer1 = new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);
            }
        };
        consumer1.accept("Hello World!");

        Consumer<String> consumer2 = (String s) -> {
            System.out.println(s);
        };
        consumer2.accept("你好，世界！");
    }

}
```



3、省略数据类型

```java
// 省略类型前代码
Consumer<String> consumer2 = (String s) -> {
    System.out.println(s);
};
consumer2.accept("你好，世界！");

// 省略类型后代码
Consumer<String> consumer3 = (s) -> {
    System.out.println(s);
};
consumer3.accept("你好，世界！");

```

> 之所以能够省略括号中的数据类型，是因为我们在 `Comsumer<String>` 处已经指定了泛型，编译器可以推断出类型，后面就不用指定具体类型了。称为**类型推断**



4、省略参数的小括号

当我们写的 `Lambda` 表达式只需要一个参数时，参数的小括号就可以省略

```java
// 省略小括号前代码
Consumer<String> consumer3 = (s) -> {
    System.out.println(s);
};
consumer3.accept("你好，世界！");
// 省略小括号后代码
Consumer<String> consumer4 = s -> {
    System.out.println(s);
};
consumer3.accept("你好，世界！");

```





5、省略return 和大括号

当 `Lambda` 表达式体只有一条语句时，如果有返回，则 return 和大括号都可以省略

```java
import java.util.Comparator;

public class LambdaDemo4 {

    public static void main(String[] args) {

        // 省略 return 和 {} 前代码
        Comparator<Integer> comparator1 = (o1, o2) -> {
            return o1.compareTo(o2);
        };
        System.out.println(comparator1.compare(12, 12));

        // 省略 return 和 {} 后代码
        Comparator<Integer> comparator2 = (o1, o2) -> o1.compareTo(o2);
        System.out.println(comparator2.compare(12, 23));

    }
}
```



 接口内部只能包含一个抽象方法，如果接口内部包含多个抽象方法，我们就无法使用 `Lambda` 表达式了，这样只包含一个抽象方法的接口，我们称为**函数式接口**



