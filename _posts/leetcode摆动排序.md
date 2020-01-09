---
title: 280.摆动排序（Wiggle Sort）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
280.Wiggle Sort
Given an unsorted array nums, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

Example:
```
Input: nums = [3,5,2,1,6,4]
Output: One possible answer is [3,5,1,6,2,4]
```

#### Solution
```java
public class Solution {
    public void wiggleSort(int[] nums) {
        if (nums == null || nums.length < 2) return;
        for (int i = 1; i < nums.length; i++) {
            if ((i % 2 == 0 && nums[i] > nums[i - 1]) || (i % 2 == 1 && nums[i] < nums[i - 1])) {
                int tmp = nums[i];
                nums[i] = nums[i - 1];
                nums[i - 1] = tmp;
            }
        }
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/wiggle-sort/)
[YRB](https://www.cnblogs.com/yrbbest/p/5035540.html)***
