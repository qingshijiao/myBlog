---
title: 322.零钱兑换 (Coin Change)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [322\. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

Difficulty: **中等**


给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 `-1`。

**示例 1:**

```
输入: coins = [1, 2, 5], amount = 11
输出: 3
解释: 11 = 5 + 5 + 1
```

**示例 2:**

```
输入: coins = [2], amount = 3
输出: -1
```

**说明**:
你可以认为每种硬币的数量是无限的。


#### Solution - dfs

Language: **Java**

```java
​class Solution {
    private int[] coins;
    private int res;
    private void dfs(int c_index, int amount, int count) {
        if (c_index < 0)
            return;
        int c = coins[c_index];
        for (int k = amount / c; k >= 0; k--) {
            int remain = amount - k * c;
            int newCount = count + k;
            if (remain == 0) {
                res = Math.min(newCount, res);
                return;
            }
            if (newCount + 1 >= res)
                return;
            dfs(c_index - 1, remain, newCount);
        }
    }

    public int coinChange(int[] coins, int amount) {
        if (amount < 0) return -1;
        if (amount == 0) return 0;
        if (coins.length == 0) return -1;
        Arrays.sort(coins);
        res = Integer.MAX_VALUE;
        this.coins = coins;
        dfs(coins.length - 1, amount, 0);
        return res == Integer.MAX_VALUE? -1 : res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/coin-change/submissions/)***
