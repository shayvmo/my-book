# 剑指 Offer 58 - II. 左旋转字符串

> 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。
>



LeetCode地址：[剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)



代码实现：

1、PHP

```php
// 使用库函数
function reverseLeftWords($s, $n) {
    return substr($s, $n - strlen($s)) . substr($s, 0, $n);
}
```



2、Go

```go
func reverseLeftWords(s string, n int) string {
	return string(s[n:]) + string(s[0: n])
}
```

