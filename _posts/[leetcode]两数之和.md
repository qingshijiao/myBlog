---
title: [leetcode] 1.两数之和 twoSum

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

> 给定 nums = [2, 7, 11, 15], target = 9
> 
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 
> 所以返回 [0, 1]

# 题解

## 官方题解
### 1.暴力法
**思想**：遍历每个元素x，并查找是否存在一个值与 target - x 相等的目标元素，j从i+1开始

    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == target - nums[i]) {
                    return new int[] { i, j };
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
	

> 复杂度分析
> 
> - 时间复杂度：O(n^2)
> - 空间复杂度：O(1)

**说明：**throw new IllegalArgumentException("No two sum solution");

抛出的异常表明向方法传递了一个不合法或不正确的参数。

### 2.两遍哈希表
**思想：**空间换时间，哈希表支持以**近似**恒定的时间进行快速查找

    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
		//数据为键，索引为值
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement) && map.get(complement) != i) {
                return new int[] { i, map.get(complement) };
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }

> 复杂度分析
> 
> - 时间复杂度：O(n)
> - 空间复杂度：O(n)

### 3.一遍哈希表
**思想：**在插入哈希表过程中判断是否满足条件，如i+j=3，只有当遍历到j时才能得出结果

    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        throw new IllegalArgumentException("No two sum solution");
    }

> 复杂度分析
> 
> - 时间复杂度：O(n)
> - 空间复杂度：O(n)

## 其他题解
### 1.耗时 1ms，内存 38MB
**思想：**整体思路和**一遍哈希表**相似。本例巧妙初始化，java数组是不提供0初始化的，该例使用array[ & ]保证了数组初始值为0（原理我也不清楚），和 一遍哈希表 相比减少了哈希表查找等所用的少量时间

    public int[] twoSum(int[] nums, int target) {
        int indexArrayMax = 2047;
        int[] indexArrays = new int[indexArrayMax + 1];
        int diff = 0;
        for (int i = 0; i < nums.length; i++) {
            diff = target - nums[i];
            if (indexArrays[diff & indexArrayMax] != 0) {
                return new int[] { indexArrays[diff & indexArrayMax] - 1, i };
            }
			//等式左边的式子初始值为0
            indexArrays[nums[i] & indexArrayMax] = i + 1;
        }
        throw new IllegalArgumentException("No two sum value");
    }

---
***参考：[领扣](https://leetcode-cn.com/problems/two-sum/solution/liang-shu-zhi-he-by-leetcode-2/)***