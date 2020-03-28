---
title: 325.和等于 k 的最长子数组长度

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目描述：
给定一个数组 nums 和一个目标值 k，找到和等于 k 的最长子数组长度。如果不存在任意一个符合要求的子数组，则返回 0。

**注意:**
 nums 数组的总和是一定在 32 位有符号整数范围之内的。

示例 1:
```
输入: nums = [1, -1, 5, -2, 3], k = 3
输出: 4 
解释: 子数组 [1, -1, 5, -2] 和等于 3，且长度最长。
```
示例 2:
```
输入: nums = [-2, -1, 2, 1], k = 1
输出: 2 
解释: 子数组 [-1, 2] 和等于 1，且长度最长。
```

**进阶:**
你能使时间复杂度在 O(n) 内完成此题吗?

#### Solution - 哈希表

Language: **Java**

```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int len = nums.length;
        Map<Integer, Integer> map = new HashMap<>();
        int sum = 0;
        int max = 0;
        for(int i=0; i<len; i++){
            sum += nums[i];
            if(sum == k) max = Math.max(max, i+1);
            if(map.containsKey(sum-k)) max = Math.max(max,i-map.get(sum-k));
            if(!map.containsKey(sum)) map.put(sum, i);
        }
        if(max > 0) return max;
        else return 0;
    }
}

```

---
***参考:
[weixin_39784818](https://blog.csdn.net/weixin_39784818/article/details/93567095)***
