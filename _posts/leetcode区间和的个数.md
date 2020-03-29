---
title: 327.区间和的个数 (Count of Range Sum)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [327\. 区间和的个数](https://leetcode-cn.com/problems/count-of-range-sum/)

Difficulty: **困难**


给定一个整数数组 `nums`，返回区间和在 `[lower, upper]` 之间的个数，包含 `lower` 和 `upper`。
区间和 `S(i, j)` 表示在 `nums` 中，位置从 `i` 到 `j` 的元素之和，包含 `i` 和 `j` (`i` ≤ `j`)。

**说明:**
最直观的算法复杂度是 _O_(_n_<sup>2</sup>) ，请在此基础上优化你的算法。

**示例:**

```
输入: nums = [-2,5,-1], lower = -2, upper = 2,
输出: 3
解释: 3个区间分别是: [0,0], [2,2], [0,2]，它们表示的和分别为: -2, -1, 2。
```


#### Solution - 归并排序

Language: **Java**

```java
​class Solution {
    public int countRangeSum(int[] nums, int lower, int upper) {
        long[] sums = new long[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            sums[i + 1] = sums[i] + nums[i];
        }
        return divideAndConquer(sums, 0, sums.length - 1, lower, upper, new long[sums.length]);
    }

    private int divideAndConquer(long[] sums, int left, int right, int lower, int upper, long[] temp) {
        if (left == right) {
            return 0;
        }

        int mid = left + right >>> 1;
        int result = divideAndConquer(sums, left, mid, lower, upper, temp) + divideAndConquer(sums, mid + 1, right, lower, upper, temp);
        result += merge(sums, left, mid, right, lower, upper, temp);
        return result;
    }

    private int merge(long[] sums, int left, int mid, int right, int lower, int upper, long[] temp) {
        int rightLow = mid + 1;
        int rightHigh = mid + 1;
        int rightIndex = mid + 1;
        int tempIndex = 0;
        int result = 0;

        for (int i = left; i <= mid; i++) {
            while (rightLow <= right && sums[rightLow] - sums[i] < lower) {
                rightLow++;
            }
            while (rightHigh <= right && sums[rightHigh] - sums[i] <= upper) {
                rightHigh++;
            }
            while (rightIndex <= right && sums[rightIndex] <= sums[i]) {
                temp[tempIndex++] = sums[rightIndex++];
            }
            temp[tempIndex++] = sums[i];
            result += rightHigh - rightLow;
        }

        while (rightIndex <= right) {
            temp[tempIndex++] = sums[rightIndex++];
        }

        while (--tempIndex >= 0) {
            sums[--rightIndex] = temp[tempIndex];
        }

        return result;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/count-of-range-sum/submissions/)***
