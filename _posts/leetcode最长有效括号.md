---
title: 32. 最长有效括号（Longest Valid Parentheses）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

示例 1:
```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

示例 2:
```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

# 题解

## 官方题解
### 1.暴力法
**思路：** 在这种方法中，我们考虑给定字符串中每种可能的非空偶数长度子字符串，检查它是否是一个有效括号字符串序列。为了检查有效性，我们使用栈的方法。

每当我们遇到一个 ‘(’ ，我们把它放在栈顶。对于遇到的每个 ‘)’ ，我们从栈中弹出一个 ‘(’ ，如果栈顶没有 ‘(’，或者遍历完整个子字符串后栈中仍然有元素，那么该子字符串是无效的。这种方法中，我们对每个偶数长度的子字符串都进行判断，并保存目前为止找到的最长的有效子字符串的长度。
```
例子:
"((())"

(( --> 无效
(( --> 无效
() --> 有效，长度为 2
)) --> 无效
((()--> 无效
(())--> 有效，长度为 4
最长长度为 4
```

```
//超出时间限制
class Solution {
    public int longestValidParentheses(String s) {
        int maxlen = 0;
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 2; j <= s.length(); j+=2) {
                if (isValid(s.substring(i, j))) {
                    maxlen = Math.max(maxlen, j - i);
                }
            }
        }
        return maxlen;
    }

    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push('(');
            } else if (!stack.empty() && stack.peek() == '(') {
                stack.pop();
            } else {
                return false;
            }
        }
        return stack.empty();
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n^2) 。从长度为 n 的字符串产生所有可能的子字符串需要的时间复杂度为 O(n^2) 。验证一个长度为 nn 的子字符串需要的时间为 O(n) 。
- 空间复杂度：O(n) 。子字符串的长度最多会需要一个深度为 n 的栈。

### 2.动态规划
**思路：** 寻找有效括号的规律
![](https://i.loli.net/2019/09/10/V3HM2mwbKzStXND.png)
![](https://i.loli.net/2019/09/10/8O9GUxy2LVkSzNQ.png)
![](https://i.loli.net/2019/09/10/uNZPlfDCY14GAtc.png)
![](https://i.loli.net/2019/09/10/TERchIXBnZa9J3s.png)


```
class Solution {
    public int longestValidParentheses(String s) {
        int maxans = 0;
        int dp[] = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxans = Math.max(maxans, dp[i]);
            }
        }
        return maxans;
    }
}
```
**复杂度分析：**
- 时间复杂度： O(n) 。遍历整个字符串一次，就可以将 dp 数组求出来。
- 空间复杂度：O(n) 。需要一个大小为 n 的 dp 数组。



### 3.栈
**思路：** 我们将遍历字符串，将索引压入栈。如果压入栈的字符和栈顶字符配对则推出栈顶元素，这样我们就实现了配对元素两两相消，栈顶元素的索引就是不能配对的最大索引。此刻 i - stack.peek() 就是其配对长度，保留出最长的长度。

![](https://i.loli.net/2019/09/10/gT1ZNYy3kxovfBF.png)
![](https://i.loli.net/2019/09/10/3klMR2ZLiyc6mop.png)
![](https://i.loli.net/2019/09/10/8A6hSHZ4ljCN1iE.png)
![](https://i.loli.net/2019/09/10/rTyLKqWz2NtQPDV.png)

```
class Solution {

    public int longestValidParentheses(String s) {
        int maxans = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.empty()) {
                    stack.push(i);
                } else {
                    maxans = Math.max(maxans, i - stack.peek());
                }
            }
        }
        return maxans;
    }
}
```
**复杂度分析：**
- 时间复杂度： O(n) 。 n 是给定字符串的长度。
- 空间复杂度：O(n) 。栈的大小最大达到 n。


### 4.两次遍历
**思路：** 从前到后，从后到前两次遍历链表。
定义两个变量 left right，记录左右括号的数量，这样如果 left = right，我们就认为能组成有效括号。
两次遍历的目的是防止出现 "((())" 这种情况。从前向后遍历记录最长长度为 2， 从后向前遍历记录最长长度为 4。

```
class Solution {
    public int longestValidParentheses(String s) {
        int left = 0, right = 0, maxlength = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxlength = Math.max(maxlength, 2 * right);
            } else if (right >= left) {
                left = right = 0;
            }
        }
        left = right = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxlength = Math.max(maxlength, 2 * left);
            } else if (left >= right) {
                left = right = 0;
            }
        }
        return maxlength;
    }
}

```
**复杂度分析：**
- 时间复杂度： O(n) 。遍历两遍字符串。
- 空间复杂度：O(1) 。仅有两个额外的变量 leftleft 和 rightright 。



## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/longest-valid-parentheses/solution/zui-chang-you-xiao-gua-hao-by-leetcode/)***
