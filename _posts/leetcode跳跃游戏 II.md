---
title: 45. 跳跃游戏 II（Jump Game II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

示例:
```
输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**说明:**
假设你总是可以到达数组的最后一个位置。


# 题解

## 官方题解
暂无

## 其他题解
### 1.贪心算法
**思路：**

```
class Solution {
    public int jump(int[] nums) {
        int end = 0;
        int maxPosition = 0;
        int steps = 0;
        for(int i = 0; i < nums.length - 1; i++){
            //找能跳的最远的
            maxPosition = Math.max(maxPosition, nums[i] + i);
            //遇到边界，就更新边界，并且步数加一
            if (i == end){
                end = maxPosition;
                steps++;
            }
        }
        return steps;
    }
}
```
**复杂度分析**
- 时间复杂度：O(n)
- 空间复杂度：O(1)


### 2.从后向前查找
**思路：**

```
class Solution {
    public int jump(int[] nums) {
        int position = nums.length - 1; //要找的位置
        int steps = 0;
        while (position != 0) { //是否到了第 0 个位置
            for (int i = 0; i < position; i++) {
                if (nums[i] >= position - i) {
                    position = i; //更新要找的位置
                    steps++;
                    break;
                }
            }
        }
        return steps;

    }
}
```
**复杂度分析**
- 时间复杂度：O(n^2)
- 空间复杂度：O(1)



---
***参考：
[windliang](https://leetcode-cn.com/problems/jump-game-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-10/)***
