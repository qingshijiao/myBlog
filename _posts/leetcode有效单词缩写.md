---
title: 408. 有效的单词缩写（Valid Word Abbreviation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
408. Valid Word Abbreviation有效的单词缩写
［抄题］：

Given a non-empty string s and an abbreviation abbr, return whether the string matches with the given abbreviation.

A string such as "word" contains only the following valid abbreviations:

["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
Notice that only the above abbreviations are valid abbreviations of the string "word". Any other string is not a valid abbreviation of "word".

Note:
Assume s contains only lowercase letters and abbr contains only lowercase letters and digits.

Example 1:
```
Given s = "internationalization", abbr = "i12iz4n":

Return true.
```

Example 2:
```
Given s = "apple", abbr = "a2e":

Return false.
```

#### Solution

Language: **Java**

```java
class Solution {
    public boolean validWordAbbreviation(String word, String abbr) {
        //ini
        int i = 0, j = 0;
        
        //while loop
        while (i < word.length() && j < abbr.length()) {
            //if letters, go on
            if (word.charAt(i) == abbr.charAt(j)) {
                ++i;
                ++j;
                continue;
            }
            //cc, first num shouldn't be 0
            if (abbr.charAt(j) <= '0' || abbr.charAt(j) > '9') return false;
            //substring of j
            int start = j;
            //control j whenever
            while (j < abbr.length() && abbr.charAt(j) >= '0' && abbr.charAt(j) <= '9') {
                ++j;
            }
            int num = Integer.valueOf(abbr.substring(start, j));
            //add to i
            i += num;
        }
        
        //return
        return (i == word.length()) && (j == abbr.length());
    }
}
```
---
***参考：
[immiao0319](https://www.cnblogs.com/immiao0319/p/8651383.html)***
