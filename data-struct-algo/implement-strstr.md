#### 实现strStr()



2021年10月18日

LeetCode地址：[实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)



思路：

一、暴力算法 BF



```java
public int strStr(String haystack, String needle) {
    int n = haystack.length(), m = needle.length();
    for (int i = 0; i + m <= n; i++) {
        boolean flag = true;
        for (int j = 0; j < m; j++) {
            if (haystack.charAt(i+j) != needle.charAt(j)) {
                flag = false;
                break;
            }
        }
        if (flag) {
            return i;
        }
    }
    return -1;
}
```





二、KMP算法



三、Sunday 算法

https://leetcode-cn.com/problems/implement-strstr/solution/python3-sundayjie-fa-9996-by-tes/