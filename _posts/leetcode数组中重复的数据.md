---
title: 442. 数组中重复的数据 (Find All Duplicates in an Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [442\. 数组中重复的数据](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

Difficulty: **中等**


给定一个整数数组 a，其中1 ≤ a[i] ≤ _n_ （_n_为数组长度）, 其中有些元素出现**两次**而其他元素出现**一次**。

找到所有出现**两次**的元素。

你可以不用到任何额外空间并在O(_n_)时间复杂度内解决这个问题吗？

**示例：**

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[2,3]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        int[] counts = new int[nums.length + 1];
        for (int number : nums) {
            counts[number]++;
        }
        for (int i = 1; i < counts.length; i++) {
            if (counts[i] == 2)
                res.add(i);
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/submissions/)***
