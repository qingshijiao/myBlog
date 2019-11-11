---
title: 166.分数到小数（Fraction to Recurring Decimal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个整数，分别表示分数的分子 numerator 和分母 denominator，以字符串形式返回小数。

如果小数部分为循环小数，则将循环的部分括在括号内。

示例 1:
```
输入: numerator = 1, denominator = 2
输出: "0.5"
```
示例 2:
```
输入: numerator = 2, denominator = 1
输出: "2"
```
示例 3:
```
输入: numerator = 2, denominator = 3
输出: "0.(6)"
```

# 题解

## 官方题解
### 1.竖式除法
**思路：**
![01.png](https://i.loli.net/2019/11/11/rV2Y6yxjsQM9OiJ.png)
![02.png](https://i.loli.net/2019/11/11/CsipnEIHP3D4Yfw.png)
```
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) {
            return "0";
        }
        StringBuilder fraction = new StringBuilder();
        // If either one is negative (not both)
        if (numerator < 0 ^ denominator < 0) {
            fraction.append("-");
        }
        // Convert to Long or else abs(-2147483648) overflows
        long dividend = Math.abs(Long.valueOf(numerator));
        long divisor = Math.abs(Long.valueOf(denominator));
        fraction.append(String.valueOf(dividend / divisor));
        long remainder = dividend % divisor;
        if (remainder == 0) {
            return fraction.toString();
        }
        fraction.append(".");
        Map<Long, Integer> map = new HashMap<>();
        while (remainder != 0) {
            if (map.containsKey(remainder)) {
                fraction.insert(map.get(remainder), "(");
                fraction.append(")");
                break;
            }
            map.put(remainder, fraction.length());
            remainder *= 10;
            fraction.append(String.valueOf(remainder / divisor));
            remainder %= divisor;
        }
        return fraction.toString();
    }
}
```

## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/fraction-to-recurring-decimal/solution/fen-shu-dao-xiao-shu-by-leetcode/)***
