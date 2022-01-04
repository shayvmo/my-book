# 栈

> 限定在表尾进行插入或删除操作的线性表。

和队列先进先出（First In First Out）刚好相反，栈遵循后进先出（Last In First Out）的原则。



- 顺序栈：顺序存储结构实现的栈

- 链栈：采用链式存储结构实现的栈



### 栈与递归



解决问题

- 阶乘
- 二阶 Fibonacci （斐波那契）数列
- 汉诺塔问题
- 括号匹配



#### 斐波那契数列

数列：1, 1, 2, 3, 5, 8, 13, 21... 

规律：后一项是前两项之和。

F(n) = n; n = 0,1
F(n) = F(n-1) + F(n-2),n >= 2;

常规解法

```php
function fibonacci(n)
{
   if (n === 1 || n === 2) {
     return 1;
   }
   return fibonacci(n - 1) + fibonacci(n - 2);
 }
```

问题：假设计算 fibonacci(10)，会计算 fibo(9) + fibo(8)，分治分别计算 fibo(9) 和 fibo(8) 时，fibo(8) 会造成重复计算，影响性能。

优化方式一：记录已计算的项

```php
function fibonacci(&$arr, $k) {
    if ($k === 1 || $k === 2) {
        return 1;
    }
    if (isset($arr[$k])) {
        return $arr[$k];
    }
    $arr[$k] = fibonacci($arr, $k-1) + fibonacci($arr, $k-2);
    return $arr[$k];
}
```



优化方式二：a[n] = a[n-1] + a[n-2]，本质上只需要记录最近前两项即可，相比优化方式一，节省内存

```php
function fibonacci($k) {
    $arr = [1, 1];
    for ($i = 3; $i <= $k; $i++) {
        $temp = $arr[0] + $arr[1];
        [$arr[0], $arr[1]] = [$arr[1], $temp];
    }
    return $arr[1];
}
```

