---
title: 315.计算右侧小于当前元素的个数 (Count of Smaller Numbers After Self)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [315\. 计算右侧小于当前元素的个数](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/)

Difficulty: **困难**


给定一个整数数组 _nums_，按要求返回一个新数组 _counts_。数组 _counts_ 有该性质： `counts[i]` 的值是  `nums[i]` 右侧小于 `nums[i]` 的元素的数量。

**示例:**

```
输入: [5,2,6,1]
输出: [2,1,1,0]
解释:
5 的右侧有 2 个更小的元素 (2 和 1).
2 的右侧仅有 1 个更小的元素 (1).
6 的右侧有 1 个更小的元素 (1).
1 的右侧有 0 个更小的元素.
```


#### Solution

Language: **Java**

```java
​class Solution {
    //private List<Integer> list = new ArrayList<>();
    public List<Integer> countSmaller(int[] nums) {
    if (nums.length == 0) {
            return new ArrayList<>();
        }
        int min = Integer.MAX_VALUE; // nums数组最小值
        for (int value : nums) {
            if (value < min) {
                min = value;
            }
        }
        for (int i = 0; i < nums.length; i++) {
            nums[i] = nums[i] - min + 1;
        }

        int max = Integer.MIN_VALUE;
        for (int value : nums) {
            if (value > max) {
                max = value;
            }
        }

        int[] BITree = new int[max + 1];
        BITree[0] = 0;
        int[] countArr = new int[nums.length];
        for (int i = nums.length - 1; i >= 0; i--) {
            int count = getSum(nums[i] - 1, BITree);
            countArr[i] = count;
            update(nums[i], BITree);
        }
        List<Integer> result = new ArrayList<>();
        for (int value : countArr) {
            result.add(value);
        }
        return result;
    }

    public static int getSum(int value, int[] BITree) { // 获得a[i]从1，value的和
        int sum = 0;
        while (value > 0) {
            sum += BITree[value];
            value -= (value & -value);
        }
        return sum;
    }

    public static void update(int value, int[] BITree) {
        while (value <= BITree.length - 1) {
            BITree[value] += 1;
            value += (value & -value);
        }
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/submissions/)***
