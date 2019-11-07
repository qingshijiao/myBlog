---
title: 159.至多包含两个不同字符的最长子串（Longest Substring with At Most Two Distinct Characters）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s ，找出 至多 包含两个不同字符的最长子串 t 。

示例 1:
```
输入: "eceba"
输出: 3
解释: t 是 "ece"，长度为3。
```
示例 2:
```
输入: "ccaabbb"
输出: 5
解释: t 是 "aabbb"，长度为5。
```
# 题解

## 官方题解
暂无

## 其他题解
### 1.HashMap记录个数
**思路：**
```
class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
        int res = 0, left = 0;
        unordered_map<char, int> m;
        for (int i = 0; i < s.size(); ++i) {
            ++m[s[i]];
            while (m.size() > 2) {
                if (--m[s[left]] == 0) m.erase(s[left]);
                ++left;
            }
            res = max(res, i - left + 1);
        }
        return res;
    }
};
```
### 2.HashMap记录字符的最新坐标
**思路：**
```
class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
        int res = 0, left = 0;
        unordered_map<char, int> m;
        for (int i = 0; i < s.size(); ++i) {
            m[s[i]] = i;
            while (m.size() > 2) {
                if (m[s[left]] == left) m.erase(s[left]);
                ++left;
            }
            res = max(res, i - left + 1);
        }
        return res;
    }
};
```
### 3.sliding window
**思路：**
```
class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
        int left = 0, right = -1, res = 0;
        for (int i = 1; i < s.size(); ++i) {
            if (s[i] == s[i - 1]) continue;
            if (right >= 0 && s[right] != s[i]) {
                res = max(res, i - left);
                left = right + 1;
            }
            right = i - 1;
        }
        return max(s.size() - left, res);
    }
};
```

### 4.多个变量
**思路：**
这里我们使用若干的变量，其中 cur 为当前最长子串的长度，first 和 second 为当前候选子串中的两个不同的字符，cntLast 为 second 字符的连续长度。我们遍历所有字符，假如遇到的字符是 first 和 second 中的任意一个，那么 cur 可以自增1，否则 cntLast 自增1，因为若是新字符的话，默认已经将 first 字符淘汰了，此时候选字符串由 second 字符和这个新字符构成，所以当前长度是 cntLast+1。然后再来更新 cntLast，假如当前字符等于 second 的话，cntLast 自增1，否则均重置为1，因为 cntLast 统计的就是 second 字符的连续长度。然后再来判断若当前字符不等于 second，则此时 first 赋值为 second， second 赋值为新字符。最后不要忘了用 cur 来更新结果 res，

```
class Solution {
public:
    int lengthOfLongestSubstringTwoDistinct(string s) {
        int res = 0, cur = 0, cntLast = 0;
        char first, second;
        for (char c : s) {
            cur = (c == first || c == second) ? cur + 1 : cntLast + 1;
            cntLast = (c == second) ? cntLast + 1 : 1;
            if (c != second) {
                first = second; second = c;
            }
            res = max(res, cur);
        }
        return res;
    }
};
```




---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/5185561.html)***
