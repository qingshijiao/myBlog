---
title: 483. 最小好进制 （Smallest Good Base）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [483\. 最小好进制](https://leetcode-cn.com/problems/smallest-good-base/)

Difficulty: **困难**


对于给定的整数 n, 如果n的k（k>=2）进制数的所有数位全为1，则称 k（k>=2）是 n 的一个_**好进制**_。

以字符串的形式给出 n, 以字符串的形式返回 n 的最小好进制。

**示例 1：**

```
输入："13"
输出："3"
解释：13 的 3 进制是 111。
```

**示例 2：**

```
输入："4681"
输出："8"
解释：4681 的 8 进制是 11111。
```

**示例 3：**

```
输入："1000000000000000000"
输出："999999999999999999"
解释：1000000000000000000 的 999999999999999999 进制是 11。
```

**提示：**

1.  n的取值范围是 [3, 10^18]。
2.  输入总是有效且没有前导 0。


#### Solution

Language: **Java**

```java
​class Solution {
    public String smallestGoodBase(String strNumber) {
        long number = Long.parseLong(strNumber);
        for (int m = 59; m >= 2; --m) {
            long k = (long) Math.pow(number, 1.0 / m);
            if (k >= 2) {
                long temporary = number;
                while (temporary > 0) {
                    if (temporary % k != 1) break;
                    temporary /= k;
                }
                if (temporary == 0) return String.valueOf(k);
            }
        }
        return String.valueOf(number - 1);
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/smallest-good-base/)***
