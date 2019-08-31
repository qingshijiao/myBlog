---
title: 22.括号生成（Generate Parentheses）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且**有效的**括号组合。

例如，给出 n = 3，生成结果为：
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```


# 题解

## 官方题解
### 1.暴力法
**思路：** 我们可以生成所有 2^(2n) 个 '(' 和 ')' 字符构成的序列。然后，我们将检查每一个是否有效。
**算法：** 为了生成所有序列，我们使用递归。长度为 n 的序列就是 '(' 加上所有长度为 n-1 的序列，以及 ')' 加上所有长度为 n-1 的序列。

为了检查序列是否为有效的，我们会跟踪 平衡，也就是左括号的数量减去右括号的数量的净值。如果这个值始终小于零或者不以零结束，该序列就是无效的，否则它是有效的。

```
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> combinations = new ArrayList();
        generateAll(new char[2 * n], 0, combinations);
        return combinations;
    }

    public void generateAll(char[] current, int pos, List<String> result) {
        if (pos == current.length) {
            if (valid(current))
                result.add(new String(current));
        } else {
            current[pos] = '(';
            generateAll(current, pos+1, result);
            current[pos] = ')';
            generateAll(current, pos+1, result);
        }
    }

    public boolean valid(char[] current) {
        int balance = 0;
        for (char c: current) {
            if (c == '(') balance++;
            else balance--;
            if (balance < 0) return false;
        }
        return (balance == 0);
    }
}
```
**复杂度分析：**
- 时间复杂度：O(2^(2n) * n)，对于 2^(2n)个序列中的每一个，我们用于建立和验证该序列的复杂度为 O(n)。
- 空间复杂度：O(2^(2n) * n)，简单地，每个序列都视作是有效的。

### 2.回溯算法
**思路：** 只有在我们知道序列仍然保持**有效**时才添加 '(' or ')'，而不是像 方法一 那样每次添加。我们可以通过跟踪到目前为止放置的左括号和右括号的数目来做到这一点，

如果我们还剩一个位置，我们可以开始放一个左括号。 如果它不超过左括号的数量，我们可以放一个右括号。
```
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList();
        backtrack(ans, "", 0, 0, n);
        return ans;
    }

    public void backtrack(List<String> ans, String cur, int open, int close, int max){
        if (cur.length() == max * 2) {
            ans.add(cur);
            return;
        }
        //每一次都有两种选择 添加左括号 有括号
        if (open < max)
            backtrack(ans, cur+"(", open+1, close, max);
        if (close < open)
            backtrack(ans, cur+")", open, close+1, max);
    }
}
```
**复杂度分析：**
- 时间复杂度：O((4 ^ n) / sqrt(n))，在回溯过程中，每个有效序列最多需要 n 步。
- 空间复杂度：O((4 ^ n) / sqrt(n))，如上所述，并使用 O(n)O(n) 的空间来存储序列。

### 3.闭合数
**思路：** 为了枚举某些内容，我们通常希望将其表示为更容易计算的不相交子集的总和。

考虑有效括号序列 S 的 闭包数：至少存在 index >= 0，使得 S[0], S[1], ..., S[2*index+1]是有效的。 显然，每个括号序列都有一个唯一的闭包号。 我们可以尝试单独列举它们。
**算法：** 对于每个闭合数 c，我们知道起始和结束括号必定位于索引 0 和 2 * c + 1。然后两者间的 2 * c 个元素一定是有效序列，其余元素一定是有效序列。

**闭合法理解:**
- 算法: 递归关系 n对有效括号序列由c 对有效括号序列和 n-c对有效括号序列组成
- n对有效括号序列 是由 "(" + $1 + ")" + $2 拼接而成, $1 表示c(0<=c< n)对有效括号序列集合中的某一个元素, $2表示剩下的n-1-c对有效括号序列构成的集合中的某一个元素. 这样说大致就能看懂程序在做什么了
- 这里要说一下为什么要ans.add("(" + left + ")" + right); 而不是ans.add(left+right)呢, 应该是因为有一种特殊的情况 如果left right(n=4) 全是()() 这种分隔的小括号 则当(left,right)为(1,3)或者(2,2)或者(3,1) 就会出现()()()()重复出现多次的情况, 而上面那种做法可以将()()()()的情况放到left=0,rigint=3的情况中,且只会出现一次, 非常nice

```
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList();
        if (n == 0) {
            ans.add("");
        } else {
            for (int c = 0; c < n; ++c)
                for (String left: generateParenthesis(c))
                    for (String right: generateParenthesis(n-1-c))
                        ans.add("(" + left + ")" + right);
        }
        return ans;
    }
}
```
**复杂度分析：**
- 时间复杂度：O((4 ^ n) / sqrt(n))
- 空间复杂度：O((4 ^ n) / sqrt(n))

## 其他题解
### 1.条件判断
**思路：** 每找到一个左括号，就在其后面添加一个"()", 最后再在开头加一个"()"，需要用 set 去重。
```
class Solution {
    public List<String> generateParenthesis(int n) {
        Set<String> res = new HashSet<String>();
        if (n == 0) {
            res.add("");
        } else {
            List<String> pre = generateParenthesis(n - 1);
            for (String str : pre) {
                for (int i = 0; i < str.length(); ++i) {
                    if (str.charAt(i) == '(') {
                        str = str.substring(0, i + 1) + "()" + str.substring(i + 1, str.length());
                        res.add(str);
                        str = str.substring(0, i + 1) +  str.substring(i + 3, str.length());
                    }
                }
                res.add("()" + str);
            }
        }
        return new ArrayList(res);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/generate-parentheses/solution/gua-hao-sheng-cheng-by-leetcode/)
[坐看落花](https://leetcode-cn.com/problems/generate-parentheses/solution/gua-hao-sheng-cheng-by-leetcode/#%E6%96%B9%E6%B3%95%E4%BA%8C%EF%BC%9A%E5%9B%9E%E6%BA%AF%E6%B3%95)
[Grandyang](https://www.cnblogs.com/grandyang/p/4444160.html)***
