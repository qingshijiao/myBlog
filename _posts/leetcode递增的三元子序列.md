---
title: 334.递增的三元子序列 (Increasing Triplet Subsequence)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [334\. 递增的三元子序列](https://leetcode-cn.com/problems/increasing-triplet-subsequence/)

Difficulty: **中等**


给定一个未排序的数组，判断这个数组中是否存在长度为 3 的递增子序列。

数学表达式如下:

> 如果存在这样的 _i, j, k, _ 且满足 0 ≤ _i_ < _j_ < _k_ ≤ _n_-1，
> 使得 _arr[i]_ < _arr[j]_ < _arr[k]_ ，返回 true ; 否则返回 false 。

**说明:** 要求算法的时间复杂度为 O(_n_)，空间复杂度为 O(_1_) 。

**示例 1:**

```
输入: [1,2,3,4,5]
输出: true
```

**示例 2:**

```
输入: [5,4,3,2,1]
输出: false
```


#### Solution

Language: **Java**

```java
​class Solution {
    public boolean increasingTriplet(int[] nums) {
        if(nums.length < 3)
            return false;
        int mx = Integer.MAX_VALUE, min = Integer.MAX_VALUE;
        for(int num: nums){
            if(num <= min)
                min = num;
            else if(num <= mx)
                mx = num;
            else
                return true;
        }
        return false;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/increasing-triplet-subsequence/submissions/)***
