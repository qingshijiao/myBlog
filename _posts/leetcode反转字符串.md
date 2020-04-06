---
title: 344.反转字符串 (Reverse String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [344\. 反转字符串](https://leetcode-cn.com/problems/reverse-string/)

Difficulty: **简单**


编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `char[]` 的形式给出。

不要给另外的数组分配额外的空间，你必须**修改输入数组**、使用 O(1) 的额外空间解决这一问题。

你可以假设数组中的所有字符都是 码表中的可打印字符。

**示例 1：**

```
输入：["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```


#### Solution - 双指针

Language: **Java**

```java
​class Solution {
    public void reverseString(char[] s) {
        char temp;
        int length = s.length;
        for (int i = 0; i < length / 2; i++) {
            temp = s[i];
            s[i] = s[length - i - 1];
            s[length - i - 1] = temp;
        }
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/reverse-string/solution/fan-zhuan-zi-fu-chuan-by-leetcode/)***
