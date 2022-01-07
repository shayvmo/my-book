#### 题目总结

1、命令行输出问题

```java
class Test {
    public static void main(String[] args) {
        int[] arr = new int[10];
        System.out.println(arr);//地址
        char[] arr1 = new char[10];
        System.out.println(arr1); // 整个字符串，重载问题
    }
}
```



2、定义一个`int`型的数组：` int[] arr = new int[]{12,3,3,34,56,77,432}; ` 让数组的每个位置上的值去除以首位置的元素，得到的结果，作为该位置上的新值。遍历新的数组。

```java
// 从尾到头
for(int i = arr.length – 1;i >= 0;i--){
	arr[i] = arr[i] / arr[0];
}
```



3、貌似考察参数传递的问题

```java
class Test {
    public static void main(String[] args) {
        int a = 10;
        int b = 10;
        method(a, b);// 需要在method方法调用后，仅打印出 a=100, b=200
        System.out.println("a=" + a);
        System.out.println("b=" + b);
    }
    
    public static void method(int a, int b) {
        // 方法一：直接输出题目所需结果，退出程序
        
        // 方法二：重写 system.out 输出
    }
}
```

