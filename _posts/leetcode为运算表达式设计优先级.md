---
title: 241.为运算表达式设计优先级（Different Ways to Add Parentheses）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [241\. 为运算表达式设计优先级](https://leetcode-cn.com/problems/different-ways-to-add-parentheses/)

Difficulty: **中等**


给定一个含有数字和运算符的字符串，为表达式添加括号，改变其运算优先级以求出不同的结果。你需要给出所有可能的组合的结果。有效的运算符号包含 `+`, `-` 以及 `*` 。

**示例 1:**

```
输入: "2-1-1"
输出: [0, 2]
解释:
((2-1)-1) = 0
(2-(1-1)) = 2
```

**示例 2:**

```
输入: "2*3-4*5"
输出: [-34, -14, -10, -10, 10]
解释:
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```


#### Solution - 分治

Language: **Java**

```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        if (memo.containsKey(input)) return memo.get(input);

        List<Integer> res = new ArrayList<>();

        for (int i = 0; i < input.length(); i++) {
            char c = input.charAt(i);
            if (c == '+' || c == '-' || c == '*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i+1));
                for (int j = 0; j < left.size(); j++) {
                    for (int k = 0; k < right.size(); k++) {
                        if (c == '+') res.add(left.get(j) + right.get(k));
                        else if (c == '-') res.add(left.get(j) - right.get(k));
                        else if (c == '*') res.add(left.get(j) * right.get(k));
                    }
                }
            }
        }
        if (res.isEmpty()) res.add(Integer.valueOf(input));
        memo.putIfAbsent(input, res);
        return res;
    }

    private HashMap<String, List<Integer>> memo = new HashMap<>();
}

```

```java
class Solution {
     public List<Integer> diffWaysToCompute(String input) {

        List<Integer> res = new LinkedList<>();

        for (int i = 0; i < input.length(); i++) {

            char ch = input.charAt(i);
            if (ch == '+' || ch == '-' || ch == '*') {

                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1));

                for (int l : left) {

                    for (int r : right) {

                        if (ch == '+')
                            res.add(l + r);
                        else if (ch == '-')
                            res.add(l - r);
                        else
                            res.add(l * r);
                    }
                }
            }
        }
        if (res.size() == 0)
            res.add(Integer.parseInt(input));
        return res;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/different-ways-to-add-parentheses/submissions/)***
