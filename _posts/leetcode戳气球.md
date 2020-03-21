---
title: 312.戳气球 (Burst Balloons)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [312\. 戳气球](https://leetcode-cn.com/problems/burst-balloons/)

Difficulty: **困难**


有 `n` 个气球，编号为`0` 到 `n-1`，每个气球上都标有一个数字，这些数字存在数组 `nums` 中。

现在要求你戳破所有的气球。每当你戳破一个气球 `i` 时，你可以获得 `nums[left] * nums[i] * nums[right]` 个硬币。 这里的 `left` 和 `right` 代表和 `i` 相邻的两个气球的序号。注意当你戳破了气球 `i` 后，气球 `left` 和气球 `right` 就变成了相邻的气球。

求所能获得硬币的最大数量。

**说明:**

*   你可以假设 `nums[-1] = nums[n] = 1`，但注意它们不是真实存在的所以并不能被戳破。
*   0 ≤ `n` ≤ 500, 0 ≤ `nums[i]` ≤ 100

**示例:**

```
输入: [3,1,5,8]
输出: 167
解释: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
     coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```


#### Solution - dp

![](https://pic.leetcode-cn.com/ea1c8224509d5ab9af5c52e7b1928d9a7e777458dfa4c86f37de7258cad54fd6-image-20200113223111619.png)

Language: **Java**

```java
​class Solution {
  class Solution {
      private int[][] dp;

      public void fill(int[] nums, int from, int to) {
          int max = 0, maxLeft, maxRight, result;
          //假设第i个气球是最后被戳破的
          for (int i = from; i <= to; i++) {
              maxLeft = dp[from][i - 1];
              maxRight = dp[i + 1][to];
              result = maxLeft + maxRight + nums[from - 1] * nums[i] * nums[to + 1];
              max = result > max ? result : max;
          }
          dp[from][to] = max;
      }

      public int maxCoins(int[] nums) {
          int length = nums.length;
          dp = new int[length + 2][length + 2];
          for (int i = length + 1; i >= 0; i--) {
              Arrays.fill(dp[i], 0);
          }

          int[] expandNums = new int[length + 2];
          expandNums[0] = expandNums[length + 1] = 1;
          System.arraycopy(nums, 0, expandNums, 1, length);

          for (int span = 0; span < length; span++) {
              //fill a diagonal
              //assume the span (of array of length i) is i-1
              for (int from = length - span; from > 0; from--) {
                  //fill dp[from][from + span]
                  fill(expandNums, from, from + span);
              }
          }
          return dp[1][length];
      }
  }
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/burst-balloons/submissions/)***
