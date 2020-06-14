---
title: 476. 数字的补数（Number Complement）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [476\. 数字的补数](https://leetcode-cn.com/problems/number-complement/)

Difficulty: **简单**


给定一个正整数，输出它的补数。补数是对该数的二进制表示取反。

**示例 1:**

```
输入: 5
输出: 2
解释: 5 的二进制表示为 101（没有前导零位），其补数为 010。所以你需要输出 2 。
```

**示例 2:**

```
输入: 1
输出: 0
解释: 1 的二进制表示为 1（没有前导零位），其补数为 0。所以你需要输出 0 。
```

**注意:**

1.  给定的整数保证在 32 位带符号整数的范围内。
2.  你可以假定二进制数不包含前导零位。
3.  本题与 1009 相同


#### Solution

Language: **Java**

```java
​class Solution {
    public int findComplement(int num) {
        int res = 1;
        while (res < num) {
            res <<= 1;
            res += 1;
        }
        return res ^ num;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/number-complement/submissions/)***
