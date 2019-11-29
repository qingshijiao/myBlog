---
title: 205.同构字符串（Isomorphic Strings）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [205\. 同构字符串](https://leetcode-cn.com/problems/isomorphic-strings/)

Difficulty: **简单**


给定两个字符串 **_s_** 和 **_t_**，判断它们是否是同构的。

如果 **_s_** 中的字符可以被替换得到 **_t_**，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

**示例 1:**

```
输入: s = "egg", t = "add"
输出: true
```

**示例 2:**

```
输入: s = "foo", t = "bar"
输出: false
```

**示例 3:**

```
输入: s = "paper", t = "title"
输出: true
```

**说明:**
你可以假设 _**s **_和 **_t_ **具有相同的长度。


#### Solution - 比较字符第一次出现的位置

Language: **Java**

```java
​class Solution {
    public boolean isIsomorphic(String s, String t) {
        char[] ch1 = s.toCharArray();
        char[] ch2 = t.toCharArray();
        int len = s.length();
        for (int i = 0; i < len; i++) {
            if(s.indexOf(ch1[i]) != t.indexOf(ch2[i])){
                return false;
            }
        }
        return true;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/isomorphic-strings/submissions/)
[众人都是孤独的](https://leetcode-cn.com/problems/isomorphic-strings/solution/javake-neng-bi-jiao-jian-dan-de-xie-fa-by-hao-fei-/)***
