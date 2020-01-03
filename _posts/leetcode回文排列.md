---
title: 266.回文排列（Palindrome Permutation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
266.Palindrome Permutation
Given a string, determine if a permutation of the string could form a palindrome.

Example 1:
```
Input: "code"
Output: false
```
Example 2:
```
Input: "aab"
Output: true
```
Example 3:
```
Input: "carerac"
Output: true
```

#### Solution - 计算单个字符的个数

Language: **Java**

```java
​public class Solution {
    public boolean canPermutePalindrome(String s) {
        if (s == null || s.length() == 0) {
            return false;
        }
        int[] bitArr = new int[256];
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            bitArr[c]++;
            count = bitArr[c] % 2 != 0 ? count + 1 : count - 1;
        }
        return count <= 1;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/palindrome-permutation/)
[YRB](https://www.cnblogs.com/yrbbest/p/5021398.html)***
