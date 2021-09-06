## 字符串匹配算法

2021年8月31日

- [BF算法](#BF)
- [KMP算法](#KMP)
- [Tire算法](#Trie)





### <a name="BF">BF算法</a>

> Brute Force 暴力匹配算法

- 主串：在字符串A寻找
- 模式串：寻找是否有字符串B

遍历比对主串A有没有存在模式串B；

主串A： a b s e 2 4 s a

模式串B：s e 3

```php
function bf(string $str, string $pattern) {
	for ($i=0; $i < mb_strlen($str); $i++) {
		for ($j=0; $j < mb_strlen($pattern); $j++) {
            // 匹配到不同的字符，终止模式串遍历，重新比对
			if (mb_substr($str, $i, 1) !== mb_substr($pattern, $j, 1)) {
				break;
			}
            // 模式串遍历完成，说明匹配成功
			if ($j == mb_strlen($pattern) - 1) {
				return true;
			}
            // 主串遍历完成，说明没有匹配，终止模式串遍历
			if ($i == mb_strlen($str) - 1) {
				break;
			}
            // 主串与模式串字符相同，后移继续比对
			$i++;
		}
	}
	return false;
}
```



### <a name="KMP">KMP算法</a>

> Knuth Morris Pratt 算法

模式串的前缀、后缀、共有元素的长度

模式串后移位数：已匹配的字符数 - 共有元素的长度

避免暴力算法每次都要重头匹配的缺点。



### <a name="Trie">Trie树算法</a>

> Trie 树，也叫「前缀树」或「字典树」，顾名思义，它是一个树形结构，专门用于处理字符串匹配，用来解决在一组字符串集合中快速查找某个字符串的问题。

适用于查找前缀匹配的字符串，比如敏感词过滤和搜索框联想功能。

子节点使用数组存储。





### 其他

单模式匹配：给定主串匹配模式串

BF、KMP



多模式匹配：多个模式串和单个主串匹配

Trie 树算法