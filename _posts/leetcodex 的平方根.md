---
title: 69. x 的平方根（Sqrt(x)）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:
```
输入: 4
输出: 2
```
示例 2:
```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842...,
     由于返回类型是整数，小数部分将被舍去。
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.二分猜数字
**思路：**
```
class Solution {
    public int mySqrt(int x) {
        long left = 0;
        long right = Integer.MAX_VALUE;
        while (left < right) {
            long mid = (left + right + 1) >> 1;
            long square = mid * mid;
            if (square > x) {
                right = mid - 1;
            } else {
                left = mid;
            }
        }
        return (int) left;
    }

}
```


### 2.牛顿迭代法
**思路：** 采用数值分析的思想，迭代求数值

```
class Solution {
    public int mySqrt(int a) {
        long x = a;
        while (x * x > a) {
            x = (x + a / x) / 2;
        }
        return (int) x;
    }

}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/sqrtx/submissions/)
[liweiwei1419](https://leetcode-cn.com/problems/sqrtx/solution/er-fen-cha-zhao-niu-dun-fa-python-dai-ma-by-liweiw/)***
