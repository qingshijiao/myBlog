---
title: 473.火柴拼正方形（Matchsticks to Square）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [473\. 火柴拼正方形](https://leetcode-cn.com/problems/matchsticks-to-square/)

Difficulty: **中等**


还记得童话《卖火柴的小女孩》吗？现在，你知道小女孩有多少根火柴，请找出一种能使用所有火柴拼成一个正方形的方法。不能折断火柴，可以把火柴连接起来，并且每根火柴都要用到。

输入为小女孩拥有火柴的数目，每根火柴用其长度表示。输出即为是否能用所有的火柴拼成正方形。

**示例 1:**

```
输入: [1,1,2,2,2]
输出: true

解释: 能拼成一个边长为2的正方形，每边两根火柴。
```

**示例 2:**

```
输入: [3,3,3,3,4]
输出: false

解释: 不能用所有火柴拼成一个正方形。
```

**注意:**

1.  给定的火柴长度和在 `0` 到 `10^9`之间。
2.  火柴数组的长度不超过15。


#### Solution

Language: **Java**

```java
​class Solution {
    public boolean makesquare(int[] nums) {
        if(nums == null || nums.length < 4) return false;
        int sum = 0;
        for(int i : nums){
            sum += i;
        }
        if(sum % 4 != 0) return false;
        int edge = sum / 4;
        Arrays.sort(nums);
        for(int i : nums){
            if(i > edge) return false;
        }
        boolean[] flag = new boolean[nums.length];
        for(int i = 0; i < 3; i++){
            for(int j = nums.length - 1; j >= 0 ; j--){
                if(!flag[j]){
                    int target = edge - nums[j];
                    flag[j] = true;
                    if(!backtrack(j - 1, nums, flag, target)) return false;
                }
            }
        }
        return true;
    }
    public boolean backtrack(int index, int[] nums, boolean[] flag, int target){
        if(target == 0) return true;
        for(int i = index; i >= 0; i--){
            if(flag[i] == false && nums[i] <= target){
                flag[i] = true;
                if(backtrack(i - 1, nums, flag, target - nums[i])) return true;
                flag[i] = false;
            }
        }
        return false; 
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/matchsticks-to-square/)***
