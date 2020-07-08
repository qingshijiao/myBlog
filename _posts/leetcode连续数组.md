---
title: 525. 连续数组（Contiguous Array）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [525\. 连续数组](https://leetcode-cn.com/problems/contiguous-array/)

Difficulty: **中等**


给定一个二进制数组, 找到含有相同数量的 0 和 1 的最长连续子数组（的长度）。

**示例 1:**

```
输入: [0,1]
输出: 2
说明: [0, 1] 是具有相同数量0和1的最长连续子数组。
```

**示例 2:**

```
输入: [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
```

**注意: **给定的二进制数组的长度不会超过50000。


#### Solution

Language: **Java**

```java
​class Solution {
    public int findMaxLength(int[] nums) {
        if (null == nums || nums.length < 2) {
            return 0;
        }

        int length = nums.length;
        int mappingLength = 2 * length + 1;
        int[] mapping = new int[mappingLength];
        for (int i = 0; i < mappingLength; i++) {
            mapping[i] = -2;
        }
        mapping[length] = -1;

        int maxLength = 0;
        int count = 0;
        for (int i = 0; i < length; i++) {
            count += 2 * nums[i] - 1;
            if (mapping[count + length] >= -1) {
                maxLength = Math.max(maxLength, i - mapping[count + length]);
            } else {
                mapping[count + length] = i;
            }
        }
        return maxLength;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/contiguous-array/)***
