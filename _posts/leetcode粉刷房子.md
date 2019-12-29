---
title: 256.粉刷房子（Paint House）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
There are a row of n houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x 3 cost matrix. For example, costs[0][0] is the cost of painting house 0 with color red; costs[1][2] is the cost of painting house 1 with color green, and so on... Find the minimum cost to paint all houses.

**Note:**
All costs are positive integers.

Example:
```
Input: [[17,2,17],[16,16,5],[14,3,19]]
Output: 10
Explanation: Paint house 0 into blue, paint house 1 into green, paint house 2 into blue.
             Minimum cost: 2 + 5 + 3 = 10.
```

#### Solution - dp数组

Language: **Java**

```java
public class Solution {
    public int minCost(int[][] costs) {
        if (costs == null || costs.length == 0) return 0;
        int pRed = 0, pGreen = 0, pBlue = 0;
        for (int[] cost : costs) {
            int lastRed = pRed, lastGreen = pGreen, lastBlue = pBlue;
            pRed = cost[0] + Math.min(lastGreen, lastBlue);
            pGreen = cost[1] + Math.min(lastRed, lastBlue);
            pBlue = cost[2] + Math.min(lastRed, lastGreen);
        }
        return Math.min(pRed, Math.min(pGreen, pBlue));
    }
}
```


---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5014958.html)***
