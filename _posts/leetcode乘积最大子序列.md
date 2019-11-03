---
title: 152.乘积最大子序列（Maximum Product Subarray）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数数组 nums ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。

示例 1:
```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```
示例 2:
```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.类似滑动窗口
**思路：**
product(i, j) = product(0, j) / product(0, i) 从数组i到j 的累乘等于 从数组开头到j的累乘除以从数组开头到i 的累乘(这里先忽略0的情况), 要考虑三种情况

- 累乘的乘积等于0,就要重新开始

- 累乘的乘积小于0, 要找到前面最大的负数, 这样才能保住从i到j最大

- 累乘的乘积大于0, 要找到前面最小的正数, 同理!




```
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums: return
        # 目前的累乘
        cur_pro = 1
        # 前面最小的正数
        min_pos = 1
        # 前面最大的负数
        max_neg = float("-inf")
        # 结果
        res = float("-inf")
        for num in nums:
            cur_pro *= num
            # 考虑三种情况
            # 大于0
            if cur_pro > 0:
                res = max(res, cur_pro // min_pos)
                min_pos = min(min_pos, cur_pro)
            # 小于0
            elif cur_pro < 0:
                if max_neg != float("-inf"):
                    res = max(res, cur_pro // max_neg)
                else:
                    res = max(res, num)
                max_neg = max(max_neg, cur_pro)
            # 等于0
            else:
                cur_pro = 1
                min_pos = 1
                max_neg = float("-inf")
                res = max(res, num)
        return res




```

### 2.动态规划
**思路：**


```
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int res = nums[0];
        int pre_max = nums[0];
        int pre_min = nums[0];
        for (int i = 1; i < nums.length; i++) {
            int cur_max = Math.max(Math.max(pre_max * nums[i], pre_min * nums[i]), nums[i]);
            int cur_min = Math.min(Math.min(pre_max * nums[i], pre_min * nums[i]), nums[i]);
            res = Math.max(res, cur_max);
            pre_max = cur_max;
            pre_min = cur_min;
        }
        return res;
    }
}


```

### 3.根据符号的个数^2
**思路：**
```
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        reverse_nums = nums[::-1]
        for i in range(1, len(nums)):
            nums[i] *= nums[i - 1] or 1
            reverse_nums[i] *= reverse_nums[i - 1] or 1
        return max(nums + reverse_nums)

```

```
class Solution {
    public int maxProduct(int[] nums) {

        int a = 1;
        int max = nums[0];

        for (int num : nums) {
            a = a * num;
            if (max < a) max = a;
            if (num == 0) a = 1;

        }
        a = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            a = a * nums[i];
            if (max < a) max = a;
            if (nums[i] == 0) a = 1;
        }
        return max;
    }
}
```

### 4.记录最小最大值
**思路：**
```
class Solution {
    public int maxProduct(int[] nums) {
          int max =Integer.MIN_VALUE,imax=1,imin=1;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i]<0){
                int temp = imax;
                imax =imin;
                imin =temp;
            }
            imax=Math.max(imax*nums[i],nums[i]);
            imin=Math.min(imin*nums[i],nums[i]);
            max=Math.max(imax,max);
        }

        return max;

    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/maximum-product-subarray/submissions/)
[powcai](https://leetcode-cn.com/problems/maximum-product-subarray/solution/duo-chong-si-lu-qiu-jie-by-powcai-3/)***
