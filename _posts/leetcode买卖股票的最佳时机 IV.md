---
title: 188.买卖股票的最佳时机 IV（Best Time to Buy and Sell Stock IV）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [188\. 买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

Difficulty: **困难**


给定一个数组，它的第 _i_ 个元素是一支给定的股票在第 _i_ 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 **k** 笔交易。

**注意:** 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [2,4,1], k = 2
输出: 2
解释: 在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。
```

**示例 2:**

```
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```


#### Solution1 - 动态规划

Language: **Java**

```
class Solution {
    public int maxProfit(int k, int[] prices) {
        int[] delta, dp, lastdp;
        int i, j, max, ans;

        if(prices.length < 2 || k == 0)
            return 0;
        delta = new int[prices.length];
        dp = new int[prices.length];
        lastdp = new int[prices.length];
        for(i = 1; i < prices.length; i++)
            delta[i] = prices[i] - prices[i-1];
        //计算出最多交易几次就能获得最大利润
        ans = 0;
        j = 0;
        for(i = 1; i < prices.length; i++){
            if(delta[i] >= 0)
                ans += delta[i];
            else
                j++;
        }
        //如果k过剩,直接返回最大值
        if(k > j)
            return ans;
        for(i = 1; i < prices.length; i++)
            dp[i] = delta[i] + (dp[i-1] > 0 ? dp[i-1] : 0);
        for(j = 1; j < k; j++){
            for(i = 1; i < prices.length; i++)
                lastdp[i] = dp[i];
            max = lastdp[0];
            for(i = 1; i < prices.length; i++){
                dp[i] = delta[i] + (dp[i-1] > max ? dp[i-1] : max);
                max = lastdp[i] > max ? lastdp[i] : max;
            }
        }
        ans = dp[0];
        for(i = 1; i < prices.length; i++)
            ans = dp[i] > ans ? dp[i] : ans;
        return ans;
    }
}
```

#### Solution2 - 股票问题总框架

Language: **Java**
[labuladong](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-w-5/)

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/repeated-dna-sequences/submissions/)
[1-12-14-18](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/solution/188-mai-mai-gu-piao-de-zui-jia-shi-ji-ivdong-tai-g/)
[labuladong](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-w-5/)***
