---
title: 541. 反转字符串 II (Reverse String II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [541\. 反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)

Difficulty: **简单**


给定一个字符串 `s` 和一个整数 `k`，你需要对从字符串开头算起的每隔 `2k` 个字符的前 `k` 个字符进行反转。

*   如果剩余字符少于 `k` 个，则将剩余字符全部反转。
*   如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

**示例:**

```
输入: s = "abcdefg", k = 2
输出: "bacdfeg"
```

**提示：**

1.  该字符串只包含小写英文字母。
2.  给定字符串的长度和 `k` 在 `[1, 10000]` 范围内。


#### Solution

Language: **Java**

```java
class Solution {
    public void reverse(char[] chars, int start, int end){
        while(start < end){
            char temp = chars[start];
            chars[start] = chars[end];
            chars[end] = temp;
            start++; end--;
        }
    }
    public String reverseStr(String s, int k) {
        char[] chars = s.toCharArray();
        for(int j = 0; j < s.length(); j += 2*k)
            reverse(chars, j, Math.min(j+k-1, s.length() - 1));
      
    
        return String.valueOf(chars);
        
        
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/reverse-string-ii/)***
