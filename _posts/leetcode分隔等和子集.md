---
title: 416. 分割等和子集 (Partition Equal Subset Sum)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [416\. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

Difficulty: **中等**


给定一个**只包含正整数**的**非空**数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**注意:**

1.  每个数组中的元素不会超过 100
2.  数组的大小不会超过 200

**示例 1:**

```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```

**示例 2:**

```
输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```


#### Solution

Language: **Java**

```java
​public class Solution {
    public boolean canPartition(int[] nums) {
       // Arrays.sort(nums);  //排序剪枝
        int sum = 0;
        for (int n : nums) sum += n;
        if (sum % 2 != 0) return false;
        sum = sum / 2;
        return getAns(nums, nums.length-1, sum, sum);
    }

    private boolean getAns(int[] nums,int index,int res1,int res2){
        if(res1 == 0 || res2 == 0) return true;
        else if(res1 < 0 || res2 < 0) return false;
        else return getAns(nums,index-1,res1-nums[index],res2) || getAns(nums,index-1,res1,res2-nums[index]);
    }
}
```
---
***参考：
[leetcode](https://leetcode-cn.com/problems/partition-equal-subset-sum/)***
