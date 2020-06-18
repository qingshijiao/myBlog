---
title: 485. 最大连续1的个数（Max Consecutive Ones）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [485\. 最大连续1的个数](https://leetcode-cn.com/problems/max-consecutive-ones/)

Difficulty: **简单**


给定一个二进制数组， 计算其中最大连续1的个数。

**示例 1:**

```
输入: [1,1,0,1,1,1]
输出: 3
解释: 开头的两位和最后的三位都是连续1，所以最大连续1的个数是 3.
```

**注意：**

*   输入的数组只包含 `0` 和`1`。
*   输入数组的长度是正整数，且不超过 10,000。


#### Solution

Language: **Java**

```java
​class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int slow = 0, quick = 0 , ret = 0,n = nums.length;
        while(quick < n){
            if (nums[quick++] == 0){
                ret = ret < quick - slow - 1 ? quick - slow - 1 : ret;
                slow = quick;//这时的quick已经不是0了。而是0的下一位，虽然可能依然是0，但问题不大
            }
        }
        return ret = ret < quick - slow ? quick - slow : ret;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/max-consecutive-ones/)***
