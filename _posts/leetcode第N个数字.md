---
title: 400.第N个数字 (Nth Digit)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [400\. 第N个数字](https://leetcode-cn.com/problems/nth-digit/)

Difficulty: **中等**


在无限的整数序列 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...中找到第 _n _个数字。

**注意:**
_n _是正数且在32位整数范围内 ( _n_ < 2<sup>31</sup>)。

**示例 1:**

```
输入:
3

输出:
3
```

**示例 2:**

```
输入:
11

输出:
0

说明:
第11个数字在序列 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... 里是0，它是10的一部分。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int findNthDigit(int n) {
        int q = 0, i = 0;
        while (0 < n - (9 * Math.pow(10, i) * (i + 1))) {
            n -= (9 * Math.pow(10, i) * (i + 1));
            q += 9 * Math.pow(10, i);
            i++;
        }
        String s = String.valueOf(q + (n + i) / (i + 1) );
        return s.charAt((n + i) % (i + 1)) - '0';
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/nth-digit/submissions/)***
