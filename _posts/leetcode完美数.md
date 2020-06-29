---
title: 507. 完美数 (Perfect Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [507\. 完美数](https://leetcode-cn.com/problems/perfect-number/)

Difficulty: **简单**


对于一个 **正整数**，如果它和除了它自身以外的所有正因子之和相等，我们称它为“完美数”。

给定一个 **整数 **`n`， 如果他是完美数，返回 `True`，否则返回 `False`

**示例：**

```
输入: 28
输出: True
解释: 28 = 1 + 2 + 4 + 7 + 14
```

**提示：**

输入的数字 **`n`** 不会超过 100,000,000\. (1e8)


#### Solution

Language: **Java**

```java
​public class Solution {
    public int pn(int p) {
        return (1 << (p - 1)) * ((1 << p) - 1);
    }
    public boolean checkPerfectNumber(int num) {
        int[] primes=new int[]{2,3,5,7,13,17,19,31};
        for (int prime: primes) {
            if (pn(prime) == num)
                return true;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num <= 0) {
            return false;
        }
        int sum = 0;
        for (int i = 1; i * i <= num; i++) {
            if (num % i == 0) {
                sum += i;
                if (i * i != num) {
                    sum += num / i;
                }

            }
        }
        return sum - num == num;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/perfect-number/)***
