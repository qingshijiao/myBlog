---
title: 150.逆波兰表达式求值（Evaluate Reverse Polish Notation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
根据逆波兰表示法，求表达式的值。

有效的运算符包括 +, -, *, / 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

**说明：**

- 整数除法只保留整数部分。
- 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。


示例 1：
```
输入: ["2", "1", "+", "3", "*"]
输出: 9
解释: ((2 + 1) * 3) = 9
```
示例 2：
```
输入: ["4", "13", "5", "/", "+"]
输出: 6
解释: (4 + (13 / 5)) = 6
```
示例 3：
```
输入: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
输出: 22
解释:
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.数组
**思路：**


```
class Solution {
    public int evalRPN(String[] tokens) {
        int[] stack = new int[tokens.length];
        int k= -1;
        for(String s : tokens) {
            switch(s) {
                case "+":
                    stack[k-1] += stack[k];
                    k--;
                    break;
                case "-":
                    stack[k-1] -= stack[k];
                    k--;
                    break;
                case "*":
                    stack[k-1] *= stack[k];
                    k--;
                    break;
                case "/":
                    stack[k-1] /= stack[k];
                    k--;
                    break;
                default:
                    stack[++k] = Integer.parseInt(s);
            }
        }
        return stack[0];
    }
}


```

### 2.栈
**思路：**

```
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        for (String s : tokens) {
            if (s.equals("+")) {
                stack.push(stack.pop() + stack.pop());
            } else if (s.equals("-")) {
                stack.push(-stack.pop() + stack.pop());
            } else if (s.equals("*")) {
                stack.push(stack.pop() * stack.pop());
            } else if (s.equals("/")) {
                int num1 = stack.pop();
                stack.push(stack.pop() / num1);
            } else {
                stack.push(Integer.parseInt(s));
            }
        }
        return stack.pop();
    }

}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/submissions/)
[StackOverflow-](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/solution/java-yi-dong-yi-jie-xiao-lu-gao-by-spirit-9-19/)***
