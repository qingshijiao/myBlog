---
title: 265.粉刷房子 II（Paint House II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
265.Paint House II
There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

**Note:**
All costs are positive integers.

Example:
```
Input: [[1,5,3],[2,9,4]]
Output: 5
Explanation: Paint house 0 into color 0, paint house 1 into color 2. Minimum cost: 1 + 4 = 5;
             Or paint house 0 into color 2, paint house 1 into color 0. Minimum cost: 3 + 2 = 5.
```

**Follow up:**
Could you solve it in O(nk) runtime?



#### Solution1 - 动态规划

Language: **Java**

```java
​public class Solution {
    public int minCostII(int[][] costs) {
        if(costs == null || costs.length == 0) {
            return 0;
        }
        int min1 = 0, min2 = 0, lastColor = -1;

        for(int i = 0; i < costs.length; i++) {
            int curMin1 = Integer.MAX_VALUE, curMin2 = Integer.MAX_VALUE, curColor = -1;
            for(int j = 0; j < costs[0].length; j++) {          // loop through all colors
                int cost = costs[i][j] + (j == lastColor ? min2 : min1);
                if(cost < curMin1) {
                    curMin2 = curMin1;
                    curColor = j;
                    curMin1 = cost;
                } else if(cost < curMin2) {
                    curMin2 = cost;
                }
            }
            min1 = curMin1;
            min2 = curMin2;
            lastColor = curColor;
        }

        return min1;
    }
}
```


#### Solution2 - 动态规划

Language: **Java**

```java
​public class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0) return 0;
        int minCost = 0, secondMinCost = 0, lastColor = -1;

        for (int[] cost : costs) {
            int curMin = Integer.MAX_VALUE, curSecondMin = Integer.MAX_VALUE, curColor = -1;
            for (int j = 0; j < cost.length; j++) {
                int curCost = cost[j] + (j == lastColor ? secondMinCost : minCost);
                if (curCost < curMin) {
                    curSecondMin = curMin;
                    curMin = curCost;
                    curColor = j;
                } else if (curCost < curSecondMin) {
                    curSecondMin = curCost;
                }
            }
            minCost = curMin;
            secondMinCost = curSecondMin;
            lastColor = curColor;
        }

        return minCost;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/paint-house-ii)
[YRB](https://www.cnblogs.com/yrbbest/p/5020937.html)***
