---
title: 28. 实现 strStr()（Implement strStr()）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:
> 输入: haystack = "hello", needle = "ll"
> 输出: 2

示例 2:
> 输入: haystack = "aaaaa", needle = "bba"
> 输出: -1

**说明:**
当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。



# 题解

## 官方题解
暂无

## 其他题解
### 1.逐个字符判断
**思路：** 逐个字符判断，全部符合退出，不符合则字符前端向后移动一个单位。
```
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0){
            return 0;
        }
        int flag = -1;
        for(int i = 0; i <= haystack.length() - needle.length(); i++){
            if(haystack.charAt(i) == needle.charAt(0)){
                flag = i;
                int j = 0;
                while(j < needle.length() && haystack.charAt(i) == needle.charAt(j)){
                    i++;
                    j++;
                }
                if(j == needle.length()){
                    return flag;
                }else{
                    i = flag;
                }
            }
        }
        return -1;
    }
}
```

---
***参考：
[领扣](https://leetcode-cn.com/problems/implement-strstr/)***
