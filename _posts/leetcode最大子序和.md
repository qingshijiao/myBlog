---
title: 53. 最大子序和（Maximum Subarray）

date: 2019-09-22 08:30
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。




# 题解

## 官方题解

## 其他题解
### 1.遍历一遍，开头为正数
**思路：**
```
class Solution {
    public int maxSubArray(int[] nums) {
        int ans = nums[0];
        int sum = 0;
        for(int num: nums) {
            if(sum > 0) {
                sum += num;
            } else {
                sum = num;
            }
            ans = Math.max(ans, sum);
        }
        return ans;
    }
}
```


### 2.分治法
**思路：** 中线划分左右两部分，计算两边最大子序和，然后从中线向左和右遍历，找出中间的最大子序和，返回三者中最大的。

```
class Solution {

  public int maxSubArrayHelper(int[] nums, int start, int end) {
      // 递归终止条件
      if (start == end) {
          return nums[start];
      }

      int mid = (start + end) / 2;
      // 递归计算左半边最大子序和
      int max_left = maxSubArrayHelper(nums, start, mid);
      // 递归计算右半边最大子序和
      int max_right = maxSubArrayHelper(nums, mid + 1, end);

      // 计算中间的最大子序和
      // 从右到左计算左边的最大子序和,
      int tmp = 0;
      int m_left = nums[mid];
      for (int i = mid; i >= start; i--) {
          tmp += nums[i];
          m_left = Math.max(tmp, m_left);
      }

      // 从左到右计算右边的最大子序和再相加
      tmp = 0;
      int m_right = nums[mid + 1];
      for (int i = mid + 1; i <= end; i++) {
          tmp += nums[i];
          m_right = Math.max(tmp, m_right);
      }

      // 返回三个中的最大值
      return Math.max(m_left + m_right, Math.max(max_left, max_right));
  }



  public int maxSubArray(int[] nums) {
      return maxSubArrayHelper(nums, 0, nums.length - 1);
  }


}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/maximum-subarray/)***
