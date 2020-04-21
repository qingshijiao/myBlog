---
title: 371.两整数之和 (Sum of Two Integers)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [371\. 两整数之和](https://leetcode-cn.com/problems/sum-of-two-integers/)

Difficulty: **简单**


**不使用**运算符 `+` 和 `-` ​​​​​​​，计算两整数 ​​​​​​​`a` 、`b` ​​​​​​​之和。

**示例 1:**

```
输入: a = 1, b = 2
输出: 3
```

**示例 2:**

```
输入: a = -2, b = 3
输出: 1
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int getSum(int a, int b) {
        while(b!=0)
        {
            int res = (a&b)<<1;
            a = a^b;
            b = res;
        }
        return a;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/sum-of-two-integers/submissions/)***
