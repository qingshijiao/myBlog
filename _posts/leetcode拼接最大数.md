---
title: 321.拼接最大数 (Create Maximum Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [321\. 拼接最大数](https://leetcode-cn.com/problems/create-maximum-number/)

Difficulty: **困难**


给定长度分别为 `m` 和 `n` 的两个数组，其元素由 `0-9` 构成，表示两个自然数各位上的数字。现在从这两个数组中选出 `k (k <= m + n)` 个数字拼接成一个新的数，要求从同一个数组中取出的数字保持其在原数组中的相对顺序。

求满足该条件的最大数。结果返回一个表示该最大数的长度为 `k` 的数组。

**说明:** 请尽可能地优化你算法的时间和空间复杂度。

**示例 1:**

```
输入:
nums1 = [3, 4, 6, 5]
nums2 = [9, 1, 2, 5, 8, 3]
k = 5
输出:
[9, 8, 6, 5, 3]
```

**示例 2:**

```
输入:
nums1 = [6, 7]
nums2 = [6, 0, 4]
k = 5
输出:
[6, 7, 6, 0, 4]
```

**示例 3:**

```
输入:
nums1 = [3, 9]
nums2 = [8, 9]
k = 3
输出:
[9, 8, 9]
```


#### Solution

Language: **Java**

```java
​class Solution {

    private int[] maxNumber(int[] nums, int k) {
        int[] res = new int[k];
        if (k == 0) return res;
        int size = 0, len = nums.length;
        for (int i = 0; i < len; i++) {
            while (size > 0 && len - i + size > k && nums[i] > res[size - 1])
                size--;
            if (size < k)
                res[size++] = nums[i];
        }
        return res;
    }

    // 比较num1从p1位置开始和num2从p2位置开始逐一比较
    private int compare(int[] num1, int p1, int[] num2, int p2) {
        for (int i = 0; p1 + i < num1.length && p2 + i < num2.length; i++) {
            if (num1[p1 + i] > num2[p2 + i]) return 1;
            if (num1[p1 + i] < num2[p2 + i]) return -1;
        }
        if (num1.length - p1 == num2.length - p2)   return 0;
        return num1.length - p1 > num2.length - p2 ? 1 : -1;
    }

    private int[] merge(int[] num1, int[] num2) {
        int[] res = new int[num1.length + num2.length];
        int i = 0, j = 0;
        while (i < num1.length && j < num2.length)
            res[i + j] = compare(num1, i, num2, j) > 0 ? num1[i++] : num2[j++];
        while (i < num1.length)
            res[i + j] = num1[i++];
        while (j < num2.length)
            res[i + j] = num2[j++];
        return res;
    }

    public int[] maxNumber(int[] nums1, int[] nums2, int k) {
        int[] res = new int[k];
        for (int i = 0; i <= k; i++) {
            if (i > nums1.length || k - i > nums2.length) continue;
            int[] num1 = maxNumber(nums1, i);
            int[] num2 = maxNumber(nums2, k - i);
            int[] cur = merge(num1, num2);
            if (compare(cur, 0, res, 0) > 0) {
                res = cur;
            }
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/create-maximum-number/submissions/)***
