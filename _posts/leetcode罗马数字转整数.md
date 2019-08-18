---
title: 13.罗马数字转整数（Roman to Integer）

date: 2019-08-17 07:50
categories:
- leetcode
tags:
- leetcode

---
# 题目
罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

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

给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

示例 1:
> 输入: "III"
> 输出: 3

示例 2:
> 输入: "IV"
> 输出: 4

示例 3:
> 输入: "IX"
> 输出: 9

示例 4:
> 输入: "LVIII"
> 输出: 58
> 解释: L = 50, V= 5, III = 3.

示例 5:
> 输入: "MCMXCIV"
> 输出: 1994
> 解释: M = 1000, CM = 900, XC = 90, IV = 4.

# 题解

## 官方题解
暂无

## 其他题解
### 1.哈希表配对
**思路：** 排序，遍历每个数（如果当前数字大于0，就退出，因为三数之和大于0），双指针（当前数字后一个， 最后一个），判断三数之和，是否等于 0 。（小于 0，前指针后移，增大和；大于 0，后指针前移，减小和。）

```
class Solution {
    public int romanToInt(String s) {
        Map<String, Integer> map = new HashMap<>();
        map.put("I", 1);
        map.put("IV", 4);
        map.put("V", 5);
        map.put("IX", 9);
        map.put("X", 10);
        map.put("XL", 40);
        map.put("L", 50);
        map.put("XC", 90);
        map.put("C", 100);
        map.put("CD", 400);
        map.put("D", 500);
        map.put("CM", 900);
        map.put("M", 1000);

        int ans = 0;
        for(int i = 0;i < s.length();) {
            if(i + 1 < s.length() && map.containsKey(s.substring(i, i+2))) {
                ans += map.get(s.substring(i, i+2));
                i += 2;
            } else {
                ans += map.get(s.substring(i, i+1));
                i ++;
            }
        }
        return ans;
    }
}
```

### 2.单个字符配对
**思路：** 这种方法优点是不占额外空间。遍历每个字符，字符比后一个表示的数大则加，小则减。
```
class Solution {
    private static int getValue(char c) {
        switch (c) {
            case 'I':
                return 1;
            case 'V':
                return 5;
            case 'X':
                return 10;
            case 'L':
                return 50;
            case 'C':
                return 100;
            case 'D':
                return 500;
            case 'M':
                return 1000;
            default:
                throw new IllegalArgumentException("Illegal character");
        }
    }

    public int romanToInt(String s) {
        int result = 0, i = 0, n = s.length();
        while (i < n) {
            int current = getValue(s.charAt(i));
            //比后一个字符大加，小减。
            if (i == n - 1 || current >= getValue(s.charAt(i + 1))) {
                result += current;
            } else {
                result -= current;
            }
            i++;
        }
        return result;
    }
}

```
### 3.
**思路：** 将特殊字符 IV 替换成其它字符 Q，用 switch 匹配


---
***参考：
[灵魂画师牧码](https://leetcode-cn.com/problems/two-sum/solution/hua-jie-suan-fa-13-luo-ma-shu-zi-zhuan-zheng-shu-b/)
[mxNHujryVX](https://leetcode-cn.com/problems/two-sum/solution/java-luo-ma-shu-zi-zhuan-zheng-shu-by-mxnhujryvx/)***
