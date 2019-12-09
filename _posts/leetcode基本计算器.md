---
title: 224.基本计算器（Basic Calculator）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [224\. 基本计算器](https://leetcode-cn.com/problems/basic-calculator/)

Difficulty: **困难**


实现一个基本的计算器来计算一个简单的字符串表达式的值。

字符串表达式可以包含左括号 `(` ，右括号 `)`，加号 `+` ，减号 `-`，**非负**整数和空格 。

**示例 1:**

```
输入: "1 + 1"
输出: 2
```

**示例 2:**

```
输入: " 2-1 + 2 "
输出: 3
```

**示例 3:**

```
输入: "(1+(4+5+2)-3)+(6+8)"
输出: 23
```

**说明：**

*   你可以假设所给定的表达式都是有效的。
*   请**不要**使用内置的库函数 `eval`。


#### Solution

Language: **Java**

```java
​class Solution {
  int pos = 0;
    public int calculate(String s) {
      if (s == null) {
        return 0;
      }
      int n = s.length();
      if (n == 0) {
        return 0;
      }
      int res = 0;
      int sign = 1;
      while (pos < n) {
        char c = s.charAt(pos);
        if (c >= '0' && c <= '9') {
          int i = pos;
          int number = 0;
          for (; i < n && s.charAt(i) >= '0' && s.charAt(i) <= '9'; i++) {
            number = number * 10 + s.charAt(i) - '0';
          }
          res += sign * number;
          sign = 1;
          pos = i - 1;
        } else if (c == ' ') {
        } else if (c == '(') {
          pos++;
          res += sign * calculate(s);
          sign = 1;
        } else if (c == ')') {
          break;
        } else if (c == '+' || c == '-') {
          sign = c == '+' ? 1 : -1;
        }
        pos++;
      }
      return res;
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/basic-calculator/submissions/)***
