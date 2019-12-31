---
title: 259.较小的三数之和（3Sum Smaller）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given an array of n integers nums and a target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.

Example:
```
Input: nums = [-2,0,1,3], and target = 2
Output: 2
Explanation: Because there are two triplets which sums are less than 2:
             [-2,0,1]
             [-2,0,3]
```
**Follow up:** Could you solve it in O(n2) runtime?

#### Solution - 排序后双指针

Language: **Java**

```java
​public class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return 0;
        Arrays.sort(nums);
        int count = 0;

        for(int i = 0; i < nums.length - 2; i++) {
            int lo = i + 1, hi = nums.length - 1;
            while(lo < hi) {
                if(nums[i] + nums[lo] + nums[hi] < target) {
                    count += hi - lo;
                    lo++;
                } else {
                    hi--;
                }
            }
        }

        return count;
    }
}
```


---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5014972.html)***
