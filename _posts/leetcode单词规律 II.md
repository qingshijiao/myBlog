---
title: 290.单词规律 II(Game of Life II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [290\. 单词规律 II](https://leetcode-cn.com/problems/word-pattern-ii/)

Difficulty: **简单**

题目描述
Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty substring in str.

Examples:
```
pattern = "abab", str = "redblueredblue" should return true.
pattern = "aaaa", str = "asdasdasdasd" should return true.
pattern = "aabb", str = "xyzabcxzyabc" should return false.
```

**Notes:**
You may assume both pattern and str contains only lowercase letters.



#### Solution - DFS

Language: **Java**

```java
​
public class Solution {
    private boolean find(char[] pattern, int step, int len, String str, String[] map, Map<String, Character> inverse) {
        if (step == pattern.length) {
            if (len == str.length()) return true;
            return false;
        }
        if (map[pattern[step] - 'a'] != null) {
            if (len + map[pattern[step] - 'a'].length() > str.length()) return false;
            if (!map[pattern[step] - 'a'].equals(str.substring(len, len + map[pattern[step] - 'a'].length()))) return false;
            return find(pattern, step + 1, len + map[pattern[step] - 'a'].length(), str, map, inverse);
        }
        int from = 1, to = (str.length() - len) - (pattern.length - 1 - step);
        if (from > to) return false;
        if (step == pattern.length - 1) from = to;
        for(int i = from; i <= to; i++) {
            String sub = str.substring(len, len + i);
            Character ch = inverse.get(sub);
            if (ch != null) continue;
            inverse.put(sub, pattern[step]);
            map[pattern[step] - 'a'] = sub;
            if (find(pattern, step + 1, len + i, str, map, inverse)) return true;
            inverse.remove(sub);
            map[pattern[step] - 'a'] = null;
        }
        return false;
    }
    public boolean wordPatternMatch(String pattern, String str) {
        return find(pattern.toCharArray(), 0, 0, str, new String[26], new HashMap<>());
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/word-pattern-ii/)
[jmspan](https://blog.csdn.net/jmspan/article/details/51165994)***
