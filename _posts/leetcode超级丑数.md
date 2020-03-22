---
title: 313.超级丑数 (Super Ugly Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [313\. 超级丑数](https://leetcode-cn.com/problems/super-ugly-number/)

Difficulty: **中等**


编写一段程序来查找第 `_n_` 个超级丑数。

超级丑数是指其所有质因数都是长度为 `k` 的质数列表 `primes` 中的正整数。

**示例:**

```
输入: n = 12, primes = [2,7,13,19]
输出: 32
解释: 给定长度为 4 的质数列表 primes = [2,7,13,19]，前 12 个超级丑数序列为：[1,2,4,7,8,13,14,16,19,26,28,32] 。
```

**说明:**

*   `1` 是任何给定 `primes` 的超级丑数。
*   给定 `primes` 中的数字以升序排列。
*   0 < `k` ≤ 100, 0 < `n` ≤ 10<sup>6</sup>, 0 < `primes[i]` < 1000 。
*   第 `n` 个超级丑数确保在 32 位有符整数范围内。


#### Solution

Language: **Java**

```java
​class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] uglyNumbers = new int[n];
        uglyNumbers[0] = 1;
        int primesNumber = primes.length, min = 1, next = 1;
        int[] primeIndexes = new int[primesNumber];
        int[] tempPrimes = new int[primesNumber];

        Arrays.fill(tempPrimes, 1);

        for (int i = 0; i < n; i++) {
            uglyNumbers[i] = min;
            min = Integer.MAX_VALUE;
            for (int j = 0; j < tempPrimes.length; j++) {
                if (tempPrimes[j] == next) {
                    tempPrimes[j] = primes[j] * uglyNumbers[primeIndexes[j]];
                    primeIndexes[j]++;
                }
                min = Math.min(tempPrimes[j], min);
            }
            next = min;
        }

        return uglyNumbers[n - 1];
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/super-ugly-number/submissions/)***
