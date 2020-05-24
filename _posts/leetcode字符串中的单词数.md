---
title: 434. 字符串中的单词数 (First Unique Character in a String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [434\. 字符串中的单词数](https://leetcode-cn.com/problems/number-of-segments-in-a-string/)

Difficulty: **简单**


统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

**示例:**

```
输入: "Hello, my name is John"
输出: 5
解释: 这里的单词是指连续的不是空格的字符，所以 "Hello," 算作 1 个单词。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int countSegments(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int count = 0;
        for (int i = 0; i < s.length(); ) {
            if (s.charAt(i) == ' ') {
                i++;
            } else {
                count++;
                i++;
                while (i < s.length()) {
                    if (s.charAt(i) != ' ' && s.charAt(i - 1) != ' ') {
                        i++;
                    } else {
                        break;
                    }
                }

            }
        }
        return count;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/number-of-segments-in-a-string/submissions/)***
