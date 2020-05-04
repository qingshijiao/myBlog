---
title: 397.整数替换 (Integer Replacement)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [397\. 整数替换](https://leetcode-cn.com/problems/integer-replacement/)

Difficulty: **中等**


给定一个正整数 _n_，你可以做如下操作：

1\. 如果 _n _是偶数，则用 `n / 2`替换 _n_。
2\. 如果 _n _是奇数，则可以用 `n + 1`或`n - 1`替换 _n_。
_n _变为 1 所需的最小替换次数是多少？

**示例 1:**

```
输入:
8

输出:
3

解释:
8 -> 4 -> 2 -> 1
```

**示例 2:**

```
输入:
7

输出:
4

解释:
7 -> 8 -> 4 -> 2 -> 1
或
7 -> 6 -> 3 -> 2 -> 1
```


#### Solution

Language: **Java**

```java
​public class Solution {
    public int integerReplacement(int c) {
        long n = c;
        int res = 0;
        while (n != 1) {
            if (n == 3){
                return res+2;
            }
            if ((n & 1) == 1) {
                if ((n & 0b11) == 0b11){
                    // 最末尾的2位为11，进行加
                    n+=1;
                }else {
                    n-=1;
                }
                res++;
            } else {
                n /= 2;
                res++;
            }
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/integer-replacement/submissions/)***
