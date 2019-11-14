---
title: 171.Excel表列序号（Excel Sheet Column Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个Excel表格中的列名称，返回其相应的列序号。

例如，
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28
    ...
```
示例 1:
```
输入: "A"
输出: 1
```
示例 2:
```
输入: "AB"
输出: 28
```
示例 3:
```
输入: "ZY"
输出: 701
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.进制转换
**思路：**
```
class Solution {
    public int titleToNumber(String s) {
        int ans = 0;
        for(int i=0;i<s.length();i++) {
            int num = s.charAt(i) - 'A' + 1;
            ans = ans * 26 + num;
        }
        return ans;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/excel-sheet-column-number/)
[guanpengchn](https://leetcode-cn.com/problems/excel-sheet-column-number/solution/hua-jie-suan-fa-171-excelbiao-lie-xu-hao-by-guanpe/)***
