---
title: 201.数字范围按位与（Bitwise AND of Numbers Range）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [201\. 数字范围按位与](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)

Difficulty: **中等**


给定范围 [m, n]，其中 0 <= m <= n <= 2147483647，返回此范围内所有数字的按位与（包含 m, n 两端点）。

**示例 1:**

```
输入: [5,7]
输出: 4
```

**示例 2:**

```
输入: [0,1]
输出: 0
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int rangeBitwiseAnd(int m, int n)
    {
        int count = 0; // 统计移位次数
        while (m != n)
        {
            m >>= 1;
            n >>= 1;
            count++;
        }
        n <<= count;
        return n;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)
[冰影星魂](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/solution/shu-zi-fan-wei-an-wei-yu-qu-qi-gao-wei-wu-bian-hua/)***
