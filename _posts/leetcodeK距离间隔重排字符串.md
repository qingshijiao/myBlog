---
title: 358.K距离间隔重排字符串 (Rearrange String k Distance Apart)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a non-empty string str and an integer k, rearrange the string such that the same characters are at least distance k from each other.

All input strings are given in lowercase letters. If it is not possible to rearrange the string, return an empty string "".

Example 1:
```
str = "aabbcc", k = 3

Result: "abcabc"

The same letters are at least distance 3 from each other.
```
Example 2:
```
str = "aaabc", k = 3

Answer: ""

It is not possible to rearrange the string.
```
Example 3:
```
str = "aaadbbcc", k = 2

Answer: "abacabcd"

Another possible answer is: "abcabcda"

The same letters are at least distance 2 from each other.
```
**Credits:**
```
Special thanks to @elmirap for adding this problem and creating all test cases.
```

#### Solution

Language: **Java**

```java
​public class Solution {
    public String rearrangeString(String str, int k) {
        if (k <= 0) return str;
        int[] f = new int[26];
        char[] sa = str.toCharArray();
        for(char c: sa) f[c-'a'] ++;
        int r = sa.length / k;
        int m = sa.length % k;
        int c = 0;
        for(int g: f) {
            if (g-r>1) return "";
            if (g-r==1) c ++;
        }
        if (c>m) return "";
        Integer[] pos = new Integer[26];
        for(int i=0; i<pos.length; i++) pos[i] = i;
        Arrays.sort(pos, new Comparator<Integer>() {
           @Override
           public int compare(Integer i1, Integer i2) {
               return f[pos[i2]] - f[pos[i1]];
           }
        });
        char[] result = new char[sa.length];
        for(int i=0, j=0, p=0; i<sa.length; i++) {
            result[j] = (char)(pos[p]+'a');
            if (-- f[pos[p]] == 0) p ++;
            j += k;
            if (j >= sa.length) {
                j %= k;
                j ++;
            }
        }
        return new String(result);
    }
}
```
---
***参考:
[lightwindy](https://www.cnblogs.com/lightwindy/p/8547310.html)***
