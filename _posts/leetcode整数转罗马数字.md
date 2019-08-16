---
title: 12.整数转罗马数字（Integer to Roman）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

```
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

- I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
- X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
- C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。

给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。

示例 1:
> 输入: 3
> 输出: "III"

示例 2:
> 输入: 4
> 输出: "IV"

示例 3:
> 输入: 9
> 输出: "IX"

示例 4:
> 输入: 58
> 输出: "LVIII"
> 解释: L = 50, V = 5, III = 3.

示例 5:
> 输入: 1994
> 输出: "MCMXCIV"
> 解释: M = 1000, CM = 900, XC = 90, IV = 4.


# 题解
> 如题意，垂直的两条线段将会与坐标轴构成一个矩形区域，较短线段的长度将会作为矩形区域的宽度，两线间距将会作为矩形区域的长度，而我们必须最大化该矩形区域的面积。

## 官方题解
暂无

## 其他题解
### 1.哈希表法
**思路：** 利用哈希表或者数组存储, 存储考虑到有可能放字符左边，所以将其一并存储。
```
class Solution {
    private String[] A = {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};
    private int[] B = {1, 4, 5, 9, 10, 40, 50, 90, 100, 400, 500, 900, 1000};

    public String intToRoman(int num) {
        StringBuilder sb = new StringBuilder();
        for (int i = A.length - 1; i >= 0; i--) {
            while (num >= B[i]) {
                sb.append(A[i]);
                num -= B[i];
            }
        }
        return sb.toString();
    }
}
```
**复杂度分析：**
- 时间复杂度：O(1)，尽管有两个循环，当循环的次数是固定的（num 不是无限大，有最大长度）
- 空间复杂度：O(1)

### 2.数学取余
**思路：** 将 num 每位的数字都用罗马数字表示。
```
class Solution {
    private String[] bit1 = new String[]{ "", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX" };
    private String[] bit10 = new String[]{ "", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC" };
    private String[] bit100 = new String[]{  "", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM" };
    private String[] bit1000 = new String[]{ "", "M", "MM", "MMM" };

    public String intToRoman(int num) {
        return bit1000[num / 1000] + bit100[num % 1000 / 100] + bit10[num % 100 / 10] + bit1[num % 10];
    }
}
```

---
***参考：
[powcai](https://leetcode-cn.com/problems/integer-to-roman/solution/ha-xi-jie-jue-by-powcai/)
[a654773927](https://leetcode-cn.com/problems/two-sum/solution/ying-gai-shi-zui-duan-zui-jian-bian-de-fang-fa-by-/)***
