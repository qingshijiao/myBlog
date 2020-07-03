---
title: 516. 最长回文子序列 (Longest Palindromic Subsequence)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [516\. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

Difficulty: **中等**


给定一个字符串 `s` ，找到其中最长的回文子序列，并返回该序列的长度。可以假设 `s` 的最大长度为 `1000` 。

**示例 1:**  
输入:

```
"bbbab"
```

输出:

```
4
```

一个可能的最长回文子序列为 "bbbb"。

**示例 2:**  
输入:

```
"cbbd"
```

输出:

```
2
```

一个可能的最长回文子序列为 "bb"。

**提示：**

*   `1 <= s.length <= 1000`
*   `s` 只包含小写英文字母


#### Solution

Language: **Java**

```java
​class Solution {
    public int longestPalindromeSubseq(String s) {
        int len = s.length();
        int dp[] = new int [len];
       
        char[] chars = s.toCharArray();
        int i,j,max;
        for(j=0;j<len;j++){
            dp[j]=1;
            max = 0;
            for(i=j-1;i>-1;i--){
                int tmp = dp[i];
                if(chars[j]==chars[i]){
                    dp[i] = max +2;
                }
                max = Math.max(tmp,max);
            }
        }
        max = 0;
        for(i = 0;i<len;i++){
            max = Math.max(max,dp[i]);
        }
 
        return max;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)***
