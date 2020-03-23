---
title: 316.去除重复字母 (Remove Duplicate Letters)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [316\. 去除重复字母](https://leetcode-cn.com/problems/remove-duplicate-letters/)

Difficulty: **困难**


给你一个仅包含小写字母的字符串，请你去除字符串中重复的字母，使得每个字母只出现一次。需保证返回结果的字典序最小（要求不能打乱其他字符的相对位置）。

**示例 1:**

```
输入: "bcabc"
输出: "abc"
```

**示例 2:**

```
输入: "cbacdcbc"
输出: "acdb"
```

**注意：**该题与 [1081](https://leetcode-cn.com/problems/smallest-subsequence-of-distinct-characters) 相同


#### Solution - 栈

![](https://pic.leetcode-cn.com/dc4e0669d1d7cbf759dc367eb1e7473a38c9d633ff70922bb20578f13f2498f0-image.png)

Language: **Java**

```java
​class Solution {
    public String removeDuplicateLetters(String s) {
        StringBuilder sb = new StringBuilder();
        char[] cs=s.toCharArray();
        int[] counts=new int[26];
        for (char c : cs) {
            counts[c-'a']++;
        }
        char[] stack=new char[26];
        boolean[] used=new boolean[26];
        int size=0;
        for (char c : cs) {
            counts[c-'a']--;
            if (used[c-'a']) {
                continue;
            }
            while (size>0 && stack[size-1]>c && counts[stack[size-1]-'a']>0) {
                used[stack[size-1]-'a']=false;
                size--;
            }
            stack[size++]=c;
            used[c-'a']=true;
        }
        for (int i=0; i<size; i++) {
            sb.append(stack[i]);
        }
        return sb.toString();
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/remove-duplicate-letters/submissions/)
[liweiwei1419](https://leetcode-cn.com/problems/remove-duplicate-letters/solution/zhan-by-liweiwei1419/)***
