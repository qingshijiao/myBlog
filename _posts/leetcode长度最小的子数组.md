---
title: 209.长度最小的子数组（Minimum Size Subarray Sum）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [209\. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

Difficulty: **中等**


给定一个含有 **n **个正整数的数组和一个正整数 **s ，**找出该数组中满足其和 **≥ s** 的长度最小的连续子数组**。**如果不存在符合条件的连续子数组，返回 0。

**示例: **

```
输入: s = 7, nums = [2,3,1,2,4,3]
输出: 2
解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
```

**进阶:**

如果你已经完成了_O_(_n_) 时间复杂度的解法, 请尝试 _O_(_n_ log _n_) 时间复杂度的解法。


#### Solution1 - 滑动窗口

Language: **Java**

```java
​class Solution {
    // 滑动窗口
    public int minSubArrayLen(int s, int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;

        int len = nums.length;
        int start = 0, end = 0;
        int sum = 0;
        int minLen = len + 1;
        while(start < len) {
            while(end < len && sum < s) {
                sum += nums[end ++];
            }
            if(sum < s)
                break;
            if(end - start < minLen) {
                minLen = end - start;
            }
            sum -= nums[start];
            ++ start;
        }
        return (minLen > len) ? 0 : minLen;
    }
}
```

#### Solution2 - 二分法

Language: **Java**

```java
​class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums.length == 0) return 0;
        for(int i = 1; i < nums.length; i++){
            nums[i] += nums[i - 1];
        }
        if(nums[nums.length - 1] < s)
            return 0;
        int result = Integer.MAX_VALUE;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] >= s) {
                result = Math.min(result, i + 1);
            }
            int index= Arrays.binarySearch(nums, 0, i,nums[i] -s);
            if(index >= 0)
            {
                result = Math.min(result, i - index);
            }else{
                index = -index -1;
                if(index >0){
                    result = Math.min(result, i - index + 1);
                }
            }
        }
        return result == Integer.MAX_VALUE ? 0: result;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/minimum-size-subarray-sum/submissions/)***
