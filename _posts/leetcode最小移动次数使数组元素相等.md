---
title: 453. 最小移动次数使数组元素相等（Minimum Moves to Equal Array Elements）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [453\. 最小移动次数使数组元素相等](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements/)

Difficulty: **简单**


给定一个长度为 _n_ 的**非空**整数数组，找到让数组所有元素相等的最小移动次数。每次移动将会使 _n_ - 1 个元素增加 1。

**示例:**

```
输入:
[1,2,3]

输出:
3

解释:
只需要3次移动（注意每次移动会增加两个元素的值）：

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```


#### Solution

Language: **Java**

```java
​class Solution {
    //n-1个民族加分 相当于 1个民族扣分~~~~
    public int minMoves(int[] nums) {
        int min = Integer.MAX_VALUE;
        for(int i =0;i<nums.length;i++) {
            if (min>nums[i])min=nums[i];
        }
        int count = 0;
        for(int i =0;i<nums.length;i++) {
            count += nums[i]-min;
        }
        return count;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements/)***
