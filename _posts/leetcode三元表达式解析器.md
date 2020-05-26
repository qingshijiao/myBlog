---
title: 439.三元表达式解析器（Ternary Expression Parser）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
Given a string representing arbitrarily nested ternary expressions, calculate the result of the expression. You can always assume that the given expression is valid and only consists of digits 0-9, ?, :, T and F (T and Frepresent True and False respectively).

Note:

The length of the given string is ≤ 10000.
Each number will contain only one digit.
The conditional expressions group right-to-left (as usual in most languages).
The condition will always be either T or F. That is, the condition will never be a digit.
The result of the expression will always evaluate to either a digit 0-9, T or F.
 

Example 1:

Input: "T?2:3"

Output: "2"

Explanation: If true, then result is 2; otherwise result is 3.
 

Example 2:

Input: "F?1:T?4:5"

Output: "4"

Explanation: The conditional expressions group right-to-left. Using parenthesis, it is read/evaluated as:

             "(F ? 1 : (T ? 4 : 5))"                   "(F ? 1 : (T ? 4 : 5))"
          -> "(F ? 1 : 4)"                 or       -> "(T ? 4 : 5)"
          -> "4"                                    -> "4"
 

Example 3:

Input: "T?T?F:5:3"

Output: "F"

Explanation: The conditional expressions group right-to-left. Using parenthesis, it is read/evaluated as:

             "(T ? (T ? F : 5) : 3)"                   "(T ? (T ? F : 5) : 3)"
          -> "(T ? F : 3)"                 or       -> "(T ? F : 5)"
          -> "F"                                    -> "F"


#### Solution

Language: **Java**

```Java
class Solution {
public:
    string parseTernary(string expression) {
        string res = expression;
        stack<int> s;
        for (int i = 0; i < expression.size(); ++i) {
            if (expression[i] == '?') s.push(i);
        }
        while (!s.empty()) {
            int t = s.top(); s.pop();
            res = res.substr(0, t - 1) + eval(res.substr(t - 1, 5)) + res.substr(t + 4);
        }
        return res;
    }
    string eval(string str) {
        if (str.size() != 5) return "";
        return str[0] == 'T' ? str.substr(2, 1) : str.substr(4);
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6022498.html)***
