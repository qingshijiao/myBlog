---
title: 395.至少有K个重复字符的最长子串 (Longest Substring with At Least K Repeating Characters)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [395\. 至少有K个重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/)

Difficulty: **中等**


找到给定字符串（由小写字符组成）中的最长子串 **_T_** ， 要求 **_T_** 中的每一字符出现次数都不少于 _k_ 。输出 **_T _**的长度。

**示例 1:**

```
输入:
s = "aaabb", k = 3

输出:
3

最长子串为 "aaa" ，其中 'a' 重复了 3 次。
```

**示例 2:**

```
输入:
s = "ababbc", k = 2

输出:
5

最长子串为 "ababb" ，其中 'a' 重复了 2 次， 'b' 重复了 3 次。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int longestSubstring(String s, int k) {
        if (s.length()<k)return 0;
        if (k<2)return s.length();
        char[] chars=s.toCharArray();
        return recursive(chars, k, 0, chars.length-1);
    }
    public int recursive(char[] chars,int target,int start,int end){
        int[] charFreq=new int[26];
        for (int i = start; i <= end; i++) {
            charFreq[chars[i]-'a']++;
        }
        while (end-start+1>target && charFreq[chars[start]-'a']<target){
            start++;
        }
        while (end-start+1>target && charFreq[chars[end]-'a']<target){
            end--;
        }
        if (end-start+1<target)return 0;
        for (int i = start; i <=end ; i++) {
            if (charFreq[chars[i]-'a']<target){
                return Math.max(recursive(chars, target, start, i-1), recursive(chars, target, i+1, end));
            }
        }

        return end-start+1;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/)***
