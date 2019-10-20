---
title: 123.买卖股票的最佳时机 III（Best Time to Buy and Sell Stock III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```
示例 2:
```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。  
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。  
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
示例 3:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。
```

# 题解

## 官方题解

## 其他题解
### 1.动态规划
**思路：**

```
public int maxProfit(int[] prices) {
    if (prices.length == 0) {
        return 0;
    }
    int dp1 = 0;
    int dp2 = 0;
    int min1 = prices[0];
    int min2 = prices[0];
    for (int i = 1; i < prices.length; i++) {
            min1 = Math.min(prices[i] - 0, min1);
            dp1 = Math.max(dp1, prices[i] - min1);

            min2 = Math.min(prices[i] - dp1, min2);
            dp2 = Math.max(dp2, prices[i] - min2);
    }
    return dp2;
}

```

### 2.状态机
**思路：**
![](https://pic.leetcode-cn.com/70b91be6eda6bb3b50a697cae0a26246aa78a7ae0f9c5045d18eaef81a4556ef.jpg)

```
class Solution {
    public int maxProfit(int[] prices){
        if (prices.length == 0){
            return 0;
        }
        int s1 = - prices[0];
        int s2 = Integer.MIN_VALUE;
        int s3 = Integer.MIN_VALUE;
        int s4 = Integer.MIN_VALUE;
        for (int i = 1; i < prices.length; i++) {
            s1 = Math.max(s1, -prices[i]); //买入价格更低的股
            s2 = Math.max(s2, s1+prices[i]); //卖出当前股，或者不操作
            s3 = Math.max(s3, s2-prices[i]); //第二次买入，或者不操作
            s4 = Math.max(s4, s3+prices[i]); //第二次卖出，或者不操作
        }
        return Math.max(0, s4);
    }
}

```

### 3.两次遍历
**思路：**
```
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int max = 0, preMin = Integer.MAX_VALUE, preMax = Integer.MIN_VALUE, n = prices.length, res = 0;
        int[] left = new int[n], right = new int[n];
        for (int i = 0; i < n; i++) {
            if (prices[i] > preMin) max = Math.max(max, prices[i] - preMin);
            else preMin = prices[i];
            left[i] = max;
        }
        max = 0;
        for (int i = n - 1; i >= 0; i--) {
            if (prices[i] < preMax) max = Math.max(max, preMax - prices[i]);
            else preMax = prices[i];
            right[i] = max;
        }
        for (int i = 0; i < n; i++) {
            int l = left[i];
            int r = i < n - 1 ? right[i + 1] : 0;
            res = Math.max(res, l + r);
        }
        return res;
    }

}
```


### 4.股票问题通解
**思路：**
![](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-wen/)

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/submissions/)
[windliang](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--29/)***
