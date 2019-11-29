---
title: 204.计数质数（Count Primes）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [204\. 计数质数](https://leetcode-cn.com/problems/count-primes/)

Difficulty: **简单**


统计所有小于非负整数 _n _的质数的数量。

**示例:**

```
输入: 10
输出: 4
解释: 小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```


#### Solution - 埃拉托色尼筛选法

Language: **Java**

```java
​class Solution {
    public int countPrimes(int n) {
        boolean [] notPrim = new boolean[n];
        int count = 0;
        for (int i = 2; i < n; i++){
            if (notPrim[i] == false) {
                count++;
                for (int j = 2; j*i < n; j++) {
                    notPrim[j*i] = true;
                }
            }
        }
        return count;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/count-primes/submissions/)***
