---
title: 493. 翻转对（Reverse Pairs）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [493\. 翻转对](https://leetcode-cn.com/problems/reverse-pairs/)

Difficulty: **困难**


给定一个数组 `nums` ，如果 `i < j` 且 `nums[i] > 2*nums[j]` 我们就将 `(i, j)` 称作一个**_重要翻转对_**。

你需要返回给定数组中的重要翻转对的数量。

**示例 1:**

```
输入: [1,3,2,3,1]
输出: 2
```

**示例 2:**

```
输入: [2,4,3,5,1]
输出: 3
```

**注意:**

1.  给定数组的长度不会超过`50000`。
2.  输入数组中的所有数字都在32位整数的表示范围内。


#### Solution

Language: **Java**

```java
​class Solution {
    int count;

    public int reversePairs(int[] nums) {
        int len = nums.length;
        sort(nums, Arrays.copyOf(nums, len), 0, len - 1);
        return count;
    }

    private void sort(int[] src, int[] dest, int s, int e) {
        if (s >= e) {
            return;
        }
        int mid = (s + e) >> 1;
        sort(dest, src, s, mid);
        sort(dest, src, mid + 1, e);
        merge(src, dest, s, mid, e);
    }

    private void merge(int[] src, int[] dest, int s, int mid, int e) {
        int i = s, j = mid + 1, k = s;
        while (i <= mid && j <= e) {
            if ((long)src[i] > 2 * ((long)src[j])) {
                count += mid - i + 1;
                j++;
            } else {
                i++;
            }
        }
        i = s;
        j = mid + 1;
        while (i <= mid && j <= e) {
            dest[k++] = src[i] <= src[j] ? src[i++] : src[j++];
        }
        while (i <= mid) {
            dest[k++] = src[i++];
        }
        while (j <= e) {
            dest[k++] = src[j++];
        }
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reverse-pairs/)***
