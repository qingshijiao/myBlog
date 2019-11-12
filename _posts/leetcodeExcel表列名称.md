---
title: 168.Excel表列名称（Excel Sheet Column Title）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
    ...
```
示例 1:
```
输入: 1
输出: "A"
```
示例 2:
```
输入: 28
输出: "AB"
```
示例 3:
```
输入: 701
输出: "ZY"
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.10 进制转 26 进制
**思路：**
```
class Solution {
    public String convertToTitle(int n) {
        String AZ = "#ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        char[] CZ = AZ.toCharArray();

        StringBuilder sb = new StringBuilder();

        while (n > 0) {
            if (n % 26 == 0) {
                sb.append("Z");
                n = n / 26 - 1;
            } else {
                sb.append(CZ[n % 26]);
                n /= 26;
            }

        }

        return sb.reverse().toString();
    }
}
```


```
class Solution {
    public String convertToTitle(int n) {
        if (n <= 0) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            n--;
            sb.append((char) (n % 26 + 'A'));
            n =n / 26;
        }
        return sb.reverse().toString();
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/excel-sheet-column-title/submissions/)***
