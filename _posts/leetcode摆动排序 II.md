---
title: 324.摆动排序 II(Wiggle Sort II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [324\. 摆动排序 II](https://leetcode-cn.com/problems/wiggle-sort-ii/)

Difficulty: **中等**


给定一个无序的数组 `nums`，将它重新排列成 `nums[0] < nums[1] > nums[2] < nums[3]...` 的顺序。

**示例 1:**

```
输入: nums = [1, 5, 1, 1, 6, 4]
输出: 一个可能的答案是 [1, 4, 1, 5, 1, 6]
```

**示例 2:**

```
输入: nums = [1, 3, 2, 2, 3, 1]
输出: 一个可能的答案是 [2, 3, 1, 3, 1, 2]
```

**说明:**
你可以假设所有输入都会得到有效的结果。

**进阶:**
你能用 O(n) 时间复杂度和 / 或原地 O(1) 额外空间来实现吗？


#### Solution - 先排序再穿插

Language: **Java**

```java
class Solution {
    public void wiggleSort(int[] nums) {
        if (nums.length < 2)
            return;
        Arrays.sort(nums);
        int len = (nums.length + 1) / 2;
        int[] fir = Arrays.copyOfRange(nums, 0, len);
        int[] sec = Arrays.copyOfRange(nums, len, nums.length);
        int index = 0;
        int i = 0, j = 0;
        for (i = sec.length - 1, j = fir.length - 1; i >= 0; i--, j--) {
            nums[index++] = fir[j];
            nums[index++] = sec[i];
        }
        if (fir.length > sec.length)
            nums[index] = fir[0];
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/wiggle-sort-ii/submissions/)***
