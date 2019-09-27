---
title: 67. 二进制求和（Add Binary）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 1 和 0。

示例 1:
```
输入: a = "11", b = "1"
输出: "100"
```
示例 2:
```
输入: a = "1010", b = "1011"
输出: "10101"
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.竖式加法
**思路：** 先从右加，不够的补零，存储时倒着存储，最后反转一下链表。
```
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder ans = new StringBuilder();
        int ca = 0;
        for(int i = a.length() - 1, j = b.length() - 1;i >= 0 || j >= 0; i--, j--) {
            int sum = ca;
            sum += i >= 0 ? a.charAt(i) - '0' : 0;
            sum += j >= 0 ? b.charAt(j) - '0' : 0;
            ans.append(sum % 2);
            ca = sum / 2;
        }
        ans.append(ca == 1 ? ca : "");
        return ans.reverse().toString();
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/plus-one/submissions/)
[guanpengchn](https://leetcode-cn.com/problems/add-binary/solution/hua-jie-suan-fa-67-er-jin-zhi-qiu-he-by-guanpengch/)***
