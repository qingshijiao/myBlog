---
title: 163.缺失区间（Missing Ranges）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
Given a sorted integer array where the range of elements are [0, 99] inclusive, return its missing ranges.
For example, given [0, 1, 3, 50, 75], return [“2”, “4->49”, “51->74”, “76->99”]


# 题解

## 官方题解
暂无

## 其他题解
### 1.逐一比较
**思路：**
```

public class Solution {
    private String range(int lower, int upper) {
        if (lower == upper) return Integer.toString(lower);
        return lower + "->" + upper;
    }
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> ranges = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            ranges.add(range(lower, upper));
            return ranges;
        }
        if (lower < nums[0]) ranges.add(range(lower, nums[0]-1));
        for(int i=0; i<nums.length-1; i++) {
            if (nums[i] + 1 < nums[i+1]) ranges.add(range(nums[i]+1, nums[i+1]-1));
        }
        if (nums[nums.length-1] < upper) ranges.add(range(nums[nums.length-1]+1, upper));
        return ranges;
    }
}
```

---
***参考：
[jmspan](https://blog.csdn.net/jmspan/article/details/51487132)***
