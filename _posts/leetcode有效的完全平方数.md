---
title: 367.有效的完全平方数 (Valid Perfect Square)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [367\. 有效的完全平方数](https://leetcode-cn.com/problems/valid-perfect-square/)

Difficulty: **简单**


给定一个正整数 _num_，编写一个函数，如果 _num_ 是一个完全平方数，则返回 True，否则返回 False。

**说明：**不要使用任何内置的库函数，如  `sqrt`。

**示例 1：**

```
输入：16
输出：True
```

**示例 2：**

```
输入：14
输出：False
```


#### Solution

Language: **Java**

```java
​class Solution {
  public boolean isPerfectSquare(int num) {
    if (num < 2) return true;

    long x = num / 2;
    while (x * x > num) {
      x = (x + num / x) / 2;
    }
    return (x * x == num);
  }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/valid-perfect-square/solution/you-xiao-de-wan-quan-ping-fang-shu-by-leetcode/)***
