---
title: 343.整数拆分 (Integer Break)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [343\. 整数拆分](https://leetcode-cn.com/problems/integer-break/)

Difficulty: **中等**


给定一个正整数 _n_，将其拆分为**至少**两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

**示例 1:**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

**说明:** 你可以假设 _n _不小于 2 且不大于 58。


#### Solution1

![](https://pic.leetcode-cn.com/1d32896766463a7a74ffafe47e7f57008e563b8fe7a8e4d52525732ac8d34275-Picture2.png)

Language: **Java**

```java
​class Solution {
    public int integerBreak(int n) {
        if(n <= 3) return n - 1;
        int a = n / 3, b = n % 3;
        if(b == 0) return (int)Math.pow(3, a);
        if(b == 1) return (int)Math.pow(3, a - 1) * 4;
        return (int)Math.pow(3, a) * 2;
    }
}
```

#### Solution2

![](https://pic.leetcode-cn.com/1d32896766463a7a74ffafe47e7f57008e563b8fe7a8e4d52525732ac8d34275-Picture2.png)

Language: **Java**

```java
class Solution {
    public int integerBreak(int n) {
        if (n <= 3) return n - 1;
        int res = 1;
        for (int i = 3; i <= n; ) {
            res *= 3;
            i += 3;
            if (i > n) {
                int a = n % 3;
                if (a == 0) return res;
                else if (a == 1) res = res / 3 * 4;
                else res *= 2;
            }
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/power-of-four/solution/4de-mi-by-leetcode/)
[Krahets](https://leetcode-cn.com/problems/integer-break/solution/343-zheng-shu-chai-fen-tan-xin-by-jyd/)***
