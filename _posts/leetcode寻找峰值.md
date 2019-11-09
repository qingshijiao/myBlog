---
title: 162.寻找峰值（Find Peak Element）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 nums，其中 nums[i] ≠ nums[i+1]，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 nums[-1] = nums[n] = -∞。

示例 1:
```
输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。
```
示例 2:
```
输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
```

**说明:**

你的解法应该是 O(logN) 时间复杂度的。



# 题解

## 官方题解
### 1.逐一判断
**思路：**
```
public class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] > nums[i + 1])
                return i;
        }
        return nums.length - 1;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)。我们对长度为 n 的数组 nums 只进行一次遍历。
- 空间复杂度： O(1)。 只使用了常数空间。


### 2.递归二分查找
**思路：**

![](https://pic.leetcode-cn.com/e2edf7bcc45863a10d438dd92b8c4c6b6b63ff834aa11f05e4a104b5cbf859fc-image.png)

![](https://pic.leetcode-cn.com/a976733e8b2e4817b2d88616b519bc58ca471ca15e9ee3f77fcc377a329e0d46-image.png)

![](https://pic.leetcode-cn.com/95f33e0a46ed380e3e5c2db5cb5a93479bb65463e7fcf6a7c953e3a039fe0461-image.png)

```
public class Solution {
    public int findPeakElement(int[] nums) {
        return search(nums, 0, nums.length - 1);
    }
    public int search(int[] nums, int l, int r) {
        if (l == r)
            return l;
        int mid = (l + r) / 2;
        if (nums[mid] > nums[mid + 1])
            return search(nums, l, mid);
        return search(nums, mid + 1, r);
    }
}

```
**复杂度分析：**
- 时间复杂度：O(log_2(n))。每一步都将搜索空间减半。因此，总的搜索空间只需要 log_2(n)步。其中 n 为 nums 数组的长度。

- 空间复杂度：O(log_2(n))。每一步都将搜索空间减半。因此，总的搜索空间只需要 log_2(n)步。于是，递归树的深度为 log_2(n)。


### 3.迭代递归
**思路：**

```
public class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0, r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] > nums[mid + 1])
                r = mid;
            else
                l = mid + 1;
        }
        return l;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(log_2(n))。每一步都将搜索空间减半。因此，总的搜索空间只需要 log_2(n)步。其中 n 为 nums 数组的长度。

- 空间复杂度：O(1)。 只使用了常数空间。




## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/find-peak-element/solution/xun-zhao-feng-zhi-by-leetcode/)***
