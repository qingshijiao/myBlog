---
title: 389.找不同 (Find the Difference)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [389\. 找不同](https://leetcode-cn.com/problems/find-the-difference/)

Difficulty: **简单**


给定两个字符串 _**s**_ 和 _**t**_，它们只包含小写字母。

字符串 **_t_** 由字符串 **_s_** 随机重排，然后在随机位置添加一个字母。

请找出在 _**t**_ 中被添加的字母。

**示例:**

```
输入：
s = "abcd"
t = "abcde"

输出：
e

解释：
'e' 是那个被添加的字母。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public char findTheDifference(String s, String t) {
        char res = 0;
        int lens = s.length();
        for (int i = 0; i < lens; i ++) {
            res ^= s.charAt(i)^ t.charAt(i);
        }
        res ^= t.charAt(lens);
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-the-difference/submissions/)***
