---
title: 522. 最长特殊序列 II (Longest Uncommon Subsequence II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [522\. 最长特殊序列 II](https://leetcode-cn.com/problems/longest-uncommon-subsequence-ii/)

Difficulty: **中等**


给定字符串列表，你需要从它们中找出最长的特殊序列。最长特殊序列定义如下：该序列为某字符串独有的最长子序列（即不能是其他字符串的子序列）。

**子序列**可以通过删去字符串中的某些字符实现，但不能改变剩余字符的相对顺序。空序列为所有字符串的子序列，任何字符串为其自身的子序列。

输入将是一个字符串列表，输出是最长特殊序列的长度。如果最长特殊序列不存在，返回 -1 。

**示例：**

```
输入: "aba", "cdc", "eae"
输出: 3
```

**提示：**

1.  所有给定的字符串长度不会超过 10 。
2.  给定字符串列表的长度将在 [2, 50 ] 之间。


#### Solution

Language: **Java**

```java
​class Solution {
    public int findLUSlength(String[] strs) {
        int n = strs.length;
        int ans = 0;
        for(int i = 0; i < n; i++){
            boolean flag = true;
            for(int j = 0; j < n; j++){
                if(i == j) continue;
                if(isSeqs(strs[i], strs[j])){
                    flag = false;
                    break;
                }
            }
            if(flag) ans = Math.max(ans, strs[i].length());
        }
        if(ans == 0) return -1;
        return ans;
    }
    public boolean isSeqs(String s1, String s2){ // a  abc
        if(s1.length() > s2.length()) return false;
        int j = 0;
        for(int i = 0; i < s2.length(); i++){
            if(s2.charAt(i) == s1.charAt(j)){
                j++;
            }
            if(j == s1.length()) break;
        }
        return j == s1.length();
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/longest-uncommon-subsequence-ii/)***
