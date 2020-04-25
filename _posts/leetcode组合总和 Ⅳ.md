---
title: 377.组合总和 Ⅳ (Combination Sum IV)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [377\. 组合总和 Ⅳ](https://leetcode-cn.com/problems/combination-sum-iv/)

Difficulty: **中等**


给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。

**示例:**

```
nums = [1, 2, 3]
target = 4

所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

请注意，顺序不同的序列被视作不同的组合。

因此输出为 7。
```

**进阶：**
如果给定的数组中含有负数会怎么样？
问题会产生什么变化？
我们需要在题目中添加什么限制来允许负数的出现？

**致谢：**
特别感谢  添加此问题并创建所有测试用例。


#### Solution

Language: **Java**

```java
​class Solution {
    private int[] dp;

    public int combinationSum4(int[] nums, int target) {
        dp = new int[target + 1];
        Arrays.fill(dp, -1);
        dp[0] = 1;
        return helper(nums, target);
    }

    private int helper(int[] nums, int target) {
        if (dp[target] != -1) {
            return dp[target];
        }
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (target >= nums[i]) {
                res += helper(nums, target - nums[i]);
            }
        }
        dp[target] = res;
        return res;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/combination-sum-iv/submissions/)***
