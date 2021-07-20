# 语法糖总结

> 记录日常使用到或碰到的语法糖


启用严格类型校验

```php
declare(strict_types=1);
```


## ?? 运算符

```php
echo $a ?? '$a';// $a
$a = 1;
echo $a ?? '$a';// 1
```

## ... 

```php
function show(array $arr, int $int, string $char)
{
    var_dump($arr, $int, $char);
}
$arr = [1,2];
$int = 1;
$char = 'a';
$param = [$arr, $int, $char];
show(...$param);// 拆分索引数组，并根据下标进行对应传参

function add(...$numbers){
    return array_sum($numbers);
}
echo add(1,2,3,4,6);// 组装成numbers数组
```


## 字符串index

```php
$string = '123456';
echo $string[0]; // 1
echo $string{1}; // 2
```

## 匿名函数

```php
$func = function (string $a) {
    echo $a;
};
$func('匿名函数');
```

## 数组批量赋值（个人理解）

左侧数组的`key`要和右侧数组`key`对应，变量才会被正确赋值，否则是`NULL`

```php
$array = [
            'title' => 'title',
            'keywords' => 'keywords',
            'description' => 'description',
        ];
[
    'title' => $title,
    'a' => $a,
] = $array;
echo $title, $a;// title, NULL
```
