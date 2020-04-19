---
title: 365.水壶问题 (Water and Jug Problem)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [365\. 水壶问题](https://leetcode-cn.com/problems/water-and-jug-problem/)

Difficulty: **中等**


有两个容量分别为 _x_升 和 _y_升 的水壶以及无限多的水。请判断能否通过使用这两个水壶，从而可以得到恰好 _z_升 的水？

如果可以，最后请用以上水壶中的一或两个来盛放取得的 _z升 _水。

你允许：

*   装满任意一个水壶
*   清空任意一个水壶
*   从一个水壶向另外一个水壶倒水，直到装满或者倒空

**示例 1:** (From the famous )

```
输入: x = 3, y = 5, z = 4
输出: True
```

**示例 2:**

```
输入: x = 2, y = 6, z = 5
输出: False
```


#### Solution

Language: **Java**

```java
​class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
            if (x + y < z) {
                return false;
            }
            if (x == 0 || y == 0) {
                if (x == z || y == z) {
                    return true;
                }
                return false;
            }
            int temp = gcd(x, y);
            return z % temp == 0;
    }

    private int gcd(int x, int y) {
        if (y == 0) {
            return x;
        }
        return gcd(y, x % y);
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/water-and-jug-problem/)***
