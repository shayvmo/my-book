# PHP 数组排序函数 sort 底层实现分析

【记录于】2021年8月3日17:39



PHP源码 github 仓库地址：[https://github.com/php/php-src](https://github.com/php/php-src)



源码路径：

```
ext\standard\array.c

Zend\zend_hash.h

Zend\zend_sort.c
```



` ext\standard\array.c `

![](D:\shayvmo\02my-book\assets\php\sort\1.png)



` Zend\zend_hash.h `

![](D:\shayvmo\02my-book\assets\php\sort\2.png)



` Zend\zend_sort.c`

![](D:\shayvmo\02my-book\assets\php\sort\3.png)

![](D:\shayvmo\02my-book\assets\php\sort\4.png)



![](D:\shayvmo\02my-book\assets\php\sort\5.png)



从上面源码可以看出，sort 函数当排序的数组元素小于等于 16 个时，采用插入排序的方式进行排序；大于 16 个元素时，采用快速排序的方式。



当元素个数小于等于 5 个时，直接使用定义的函数进行简单排序交换。