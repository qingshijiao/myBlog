---
title: 16.最接近的三数之和（3Sum Closest）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

> 例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.
> 与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).


# 题解

## 官方题解
暂无

## 其他题解
### 1.排序和双指针
**思路：** 和三数之和一样，只不过将和为 0，改为了 target

```
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int ans = nums[0] + nums[1] + nums[2];
        for(int i=0;i<nums.length-2;i++) {
            int start = i+1, end = nums.length - 1;
            while(start < end) {
                int sum = nums[start] + nums[end] + nums[i];
                if(Math.abs(target - sum) < Math.abs(target - ans))
                    ans = sum;
                if(sum > target)
                    end--;
                else if(sum < target)
                    start++;
                else
                    return ans;
            }
        }
        return ans;
    }
}

```
> **复杂度分析：**
> - 时间复杂度：O(nlgn) + O(n^2) = O(n^2)
> - 空间复杂度：O(1)


---
***参考：
[灵魂画师牧码](https://leetcode-cn.com/problems/two-sum/solution/hua-jie-suan-fa-16-zui-jie-jin-de-san-shu-zhi-he-b/)***
