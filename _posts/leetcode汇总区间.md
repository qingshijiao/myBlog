---
title: 228.汇总区间（Summary Ranges）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [228\. 汇总区间](https://leetcode-cn.com/problems/summary-ranges/)

Difficulty: **中等**


给定一个无重复元素的有序整数数组，返回数组区间范围的汇总。

**示例 1:**

```
输入: [0,1,2,4,5,7]
输出: ["0->2","4->5","7"]
解释: 0,1,2 可组成一个连续的区间; 4,5 可组成一个连续的区间。
```

**示例 2:**

```
输入: [0,2,3,4,6,8,9]
输出: ["0","2->4","6","8->9"]
解释: 2,3,4 可组成一个连续的区间; 8,9 可组成一个连续的区间。
```


#### Solution

Language: **Java**

```java
​public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> summary = new ArrayList<>();
        for (int i, j = 0; j < nums.length; ++j){
            i = j;
            // try to extend the range [nums[i], nums[j]]
            while (j + 1 < nums.length && nums[j + 1] == nums[j] + 1)
                ++j;
            // put the range into the list
            if (i == j)
                summary.add(nums[i] + "");
            else
                summary.add(nums[i] + "->" + nums[j]);
        }
        return summary;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/summary-ranges/)***
