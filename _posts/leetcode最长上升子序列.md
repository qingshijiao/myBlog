---
title: 300.最长上升子序列(Longest Increasing Subsequence)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [300\. Longest Increasing Subsequence](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

Difficulty: **中等**


给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**

```
输入: [10,9,2,5,3,7,101,18]
输出: 4
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```

**说明:**

*   可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
*   你算法的时间复杂度应该为 O(_n<sup>2</sup>_) 。

**进阶:** 你能将算法的时间复杂度降低到 O(_n_ log _n_) 吗?


#### Solution1 - 动态规划

![](https://pic.leetcode-cn.com/Figures/300_LISSlide12.PNG)

Language: **Java**
time:O(n^2) space:(n)
```java
​public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int maxans = 1;
        for (int i = 1; i < dp.length; i++) {
            int maxval = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    maxval = Math.max(maxval, dp[j]);
                }
            }
            dp[i] = maxval + 1;
            maxans = Math.max(maxans, dp[i]);
        }
        return maxans;
    }
}
```

#### Solution2 - 贪心加二分查找

考虑一个简单的贪心，如果我们要使上升子序列尽可能的长，则我们需要让序列上升得尽可能慢，因此我们希望每次在上升子序列最后加上的那个数尽可能的小。

![](https://pic.leetcode-cn.com/Figures/300_LISSlide12.PNG)


```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) return 0;
        int[] dp = new int[nums.length];
        int res = 0;
        for (int i = 0; i < nums.length; i++){
            int position = Arrays.binarySearch(dp, 0, res, nums[i]);
            if (position < 0){
                position = -position -1;
                dp[position] = nums[i];
            }
            if (position == res){
                res++;
            }
        }
        return res;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-by-leetcode-soluti/)***
