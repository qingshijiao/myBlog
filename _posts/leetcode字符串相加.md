---
title: 415. 字符串相加 (Add Strings)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [415\. 字符串相加](https://leetcode-cn.com/problems/add-strings/)

Difficulty: **简单**


给定两个字符串形式的非负整数 `num1` 和`num2` ，计算它们的和。

**注意：**

1.  `num1` 和`num2` 的长度都小于 5100.
2.  `num1` 和`num2` 都只包含数字 `0-9`.
3.  `num1` 和`num2` 都不包含任何前导零。
4.  **你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。**


#### Solution

Language: **Java**

```java
​class Solution {
    public String addStrings(String num1, String num2) {
        int len = Math.max(num1.length(), num2.length());
        char[] c1 = new char[len+1];
        char[] c2 = new char[len+1];
        for(int i = 0; i < len+1; i ++) {c1[i] = '0'; c2[i] = '0';}
        for(int i = num1.length()-1; i >= 0; i--) c1[num1.length()-i-1] = num1.charAt(i);
        for(int i = num2.length()-1; i >= 0; i--) c2[num2.length()-i-1] = num2.charAt(i);
        int h = 0;
        for(int i = 0; i < len; i++) {
            int t = h + (c1[i]-'0') + (c2[i]-'0');
            int a = t % 10;
            h = t / 10;
            c1[i] = (char)('0' + a);
        }
        if(h != 0) {
            c1[len] = '1';
            len ++;
        }
        
        StringBuilder sb = new StringBuilder();
        for(int i = len-1; i >= 0; i--) {
            sb.append(c1[i]);
        }
        return sb.toString();
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/add-strings/submissions/)***
