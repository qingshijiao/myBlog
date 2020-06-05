---
title: 459. 重复的子字符串（Repeated Substring Pattern）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [459\. 重复的子字符串](https://leetcode-cn.com/problems/repeated-substring-pattern/)

Difficulty: **简单**


给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

**示例 1:**

```
输入: "abab"

输出: True

解释: 可由子字符串 "ab" 重复两次构成。
```

**示例 2:**

```
输入: "aba"

输出: False
```

**示例 3:**

```
输入: "abcabcabcabc"

输出: True

解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)
```


#### Solution

Language: **Java**

```java
​class Solution { 
    public boolean repeatedSubstringPattern(String s) { 
        return (s + s).indexOf(s, 1) != s.length(); 
    } 
}
```

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
         int n=s.length();
         if(s==null||n<2)return false;
         for(int i=n/2;i>=1;i--){
         boolean b=true;
             if(n%i==0){
                 for(int j=n/i;j>0;j--){
                     if(!s.substring(0,i).equals(s.substring(i*(j-1),i*j))){
                        b= false;
                        break;
                     }
                 }if(b)return true;
             }
         }
         return false;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/repeated-substring-pattern/)***
