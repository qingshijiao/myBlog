---
title: 424. 替换后的最长重复字符 (Longest Repeating Character Replacement)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [424\. 替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

Difficulty: **中等**


给你一个仅由大写英文字母组成的字符串，你可以将任意位置上的字符替换成另外的字符，总共可最多替换 _k _次。在执行上述操作后，找到包含重复字母的最长子串的长度。

**注意:**  
字符串长度 和 _k_ 不会超过 10<sup>4</sup>。

**示例 1:**

```
输入:
s = "ABAB", k = 2

输出:
4

解释:
用两个'A'替换为两个'B',反之亦然。
```

**示例 2:**

```
输入:
s = "AABABBA", k = 1

输出:
4

解释:
将中间的一个'A'替换为'B',字符串变为 "AABBBBA"。
子串 "BBBB" 有最长重复字母, 答案为 4。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int characterReplacement(String s, int k) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int n = s.length();
        int l = 0;
        int ans = 0;
        int maxCnt = 0;
        int[] count = new int[128];
        for(int r = 0; r < n; r++) {
            maxCnt = Math.max(maxCnt, ++count[s.charAt(r)]);
            
            //如果maxCnt + k 小于当前的窗口的长度， 那么说明窗口太大了， 需要把 l 右移
            while (maxCnt + k < r - l + 1) {
                count[s.charAt(l)]--;
                l++;
            }            
            ans = Math.max(ans, r - l + 1);
        }
        return ans;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/longest-repeating-character-replacement/submissions/)***
