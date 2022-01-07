# 常用函数小记

## 保留小数位

- 格式化字符串
> 可以实现四舍五入
```php
sprintf( string $format[, mixed $...] ) : string

#  format格式
#  %[flags][width][.precision]specifier
```

例如：
```php
echo sprintf("%a1.8f\n", 1.684222);// '1.68'
echo sprintf("%.2f\n", 1.685222);// '1.69'
echo sprintf("%'.09d\n", 123);// '000000123'
```

- 格式化数字
> 以千位分隔符方式格式化一个数字
```php
number_format( float $number[, int $decimals = 0] ) : string

number_format( float $number, int $decimals = 0, string $dec_point = ".", string $thousands_sep = ",") : string
```

例如：
```php
$number = 1234.56;
number_format($number);// 1,235
number_format($number, 1);// 1,234.6
number_format($number, 1, ',', '-');// 1-234,6
```

- 四舍五入
> round()
```php
round( float $val[, int $precision = 0[, int $mode = PHP_ROUND_HALF_UP]] ) : float
```

第三个参数说明

| 名称 | 说明 |
| --- | --- |
| PHP_ROUND_HALF_UP | 舍入位中间值向上取值 |
| PHP_ROUND_HALF_DOWN | 舍入位中间值向下取值 |
| PHP_ROUND_HALF_EVEN | 舍入位为奇数，遵循UP，偶数遵循DOWN |
| PHP_ROUND_HALF_ODD | 舍入位为偶数，遵循UP，偶数遵循DOWN |

例如：
```php
echo round(3.4);         // 3
echo round(3.5);         // 4
echo round(3.6, 0);      // 4
echo round(1.95583, 2);  // 1.96
echo round(1241757, -3); // 1242000
echo round(5.045, 2);    // 5.05
echo round(5.055, 2);    // 5.06
echo round(5.055, 2, PHP_ROUND_HALF_UP);    // 5.06
echo round(5.055, 2, PHP_ROUND_HALF_DOWN);    // 5.05
echo round(5.055, 2, PHP_ROUND_HALF_EVEN);    // 5.06
echo round(5.045, 2, PHP_ROUND_HALF_EVEN);    // 5.04
echo round(5.045, 2, PHP_ROUND_HALF_ODD);    // 5.05
echo round(5.075, 2, PHP_ROUND_HALF_ODD);    // 5.07
```

- 取整
> floor() 舍去法取整（向下取整）
> ceil() 进一法取整（向上取整）

```php
floor( float $value) : float

ceil( float $value) : float
```

例如：
```php
echo floor(4.3);   // 4
echo floor(9.999); // 9
echo floor(-3.14); // -4

echo ceil(4.3);    // 5
echo ceil(9.999);  // 10
echo ceil(-3.14);  // -3
```
