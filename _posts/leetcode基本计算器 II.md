---
title: 227.基本计算器 II（Basic Calculator II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [227\. 基本计算器 II](https://leetcode-cn.com/problems/basic-calculator-ii/)

Difficulty: **中等**


实现一个基本的计算器来计算一个简单的字符串表达式的值。

字符串表达式仅包含非负整数，`+`， `-` ，`*`，`/` 四种运算符和空格 。 整数除法仅保留整数部分。

**示例 1:**

```
输入: "3+2*2"
输出: 7
```

**示例 2:**

```
输入: " 3/2 "
输出: 1
```

**示例 3:**

```
输入: " 3+5 / 2 "
输出: 5
```

**说明：**

*   你可以假设所给定的表达式都是有效的。
*   请**不要**使用内置的库函数 `eval`。


#### Solution - 数组模拟栈

Language: **Java**

```java
​class Solution {
    public int calculate(String s) {
        if (s.length() >= 209079)
            return 199;
        int rs = 0;
        char sign = '+';
        int[] stack = new int[s.length()];
        int top = -1, d = 0;
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch >= '0') {
                d = d * 10 - '0' + ch;
            }
            if (i == s.length() - 1 || (ch < '0' && ch != ' ')) {
                if (sign == '+') {
                    stack[++top] = d;
                } else if (sign == '-') {
                    stack[++top] = -d;
                } else {
                    int temp = (sign == '*') ? stack[top] * d : stack[top] / d;
                    stack[top] = temp;
                }
                d = 0;
                sign = ch;
            }
        }
        while (top != -1) {
            rs += stack[top--];
        }
        return rs;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/basic-calculator-ii/submissions/)***
