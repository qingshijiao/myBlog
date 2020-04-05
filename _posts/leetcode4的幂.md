---
title: 342.4的幂 (Power of Four)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [342\. 4的幂](https://leetcode-cn.com/problems/power-of-four/)

Difficulty: **简单**


给定一个整数 (32 位有符号整数)，请编写一个函数来判断它是否是 4 的幂次方。

**示例 1:**

```
输入: 16
输出: true
```

**示例 2:**

```
输入: 5
输出: false
```

**进阶：**
你能不使用循环或者递归来完成本题吗？


#### Solution

Language: **Java**

```java
​class Solution {
    public boolean isPowerOfFour(int num) {
        return (num > 0) && ((num & (num - 1)) == 0) && (num % 3 == 1);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/power-of-four/solution/4de-mi-by-leetcode/)***
