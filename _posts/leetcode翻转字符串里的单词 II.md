---
title: 186.翻转字符串里的单词 II（Reverse Words in a String II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given an input string , reverse the string word by word.

Example:
```
Input:  ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]
Output: ["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```
Note:

- A word is defined as a sequence of non-space characters.
- The input string does not contain leading or trailing spaces.
- The words are always separated by a single space.


Follow up: Could you do it in-place without allocating extra space?

#### Solution

Language: **Java**

```java
String reverseWords(String s) {
return String.join(" ", Collections.reverse(Arrays.asList(s.split(" "))));
}

​
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reverse-words-in-a-string-ii/)
[grandyang](https://www.cnblogs.com/grandyang/p/5186294.html)***
