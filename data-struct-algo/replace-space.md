# 替换空格

> 请实现一个函数，把字符串中的每个空格替换成"%20"。例如输入“We are happy.”，则输出“We%20are%20happy.”。



LeetCode地址：[https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)



在原来的字符串上替换，并且保证输入的字符串后面有足够的多的空余内存



代码实现：

1、PHP

```php
// 库函数
function replaceSpace($s) {
    return str_replace(' ', '%20', $s);
}

// 算法
function replaceSpace($s) {
    $len = strlen($s);
    if ($len === 0) {
        return $s;
    }
    $newLen = strlen($s);
    for ($i=0;$i < $len;$i++) {
        if ($s[$i] === ' ') {
            $newLen += 2;
        }
    }

    for ($i=$len-1; $i >= 0; $i--) {
        if ($s[$i] === ' ') {
            $s[$newLen - 1] = '0';
            $s[$newLen - 2] = '2';
            $s[$newLen - 3] = '%';
            $newLen -= 3;
        } else {
            $s[$newLen - 1] = $s[$i];
            $newLen--;
        }
    }
    return $s;
}
```



2、Go

```go
// 库函数
func replaceSpace(s string) string {
	return strings.Replace(s, " ", "%20", -1)
}

// 算法, 待完成
func replaceSpace(s string) string {
	
}
```



