---
title: 88.合并两个有序数组（Merge Sorted Array）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
示例:
```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

# 题解

## 官方题解
### 1.合并后排序
**思路：**
最朴素的解法就是将两个数组合并之后再排序。该算法只需要一行(Java是2行)，时间复杂度较差，为 O((n+m)log(n+m))。这是由于这种方法没有利用两个数组本身已经有序这一点。



```
class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    System.arraycopy(nums2, 0, nums1, m, n);
    Arrays.sort(nums1);
  }
}

```
**复杂度分析：**
- 时间复杂度：O((n+m)log(n+m))。
- 空间复杂度：O(1)。

### 2.双指针-从前向后
**思路：**
![](https://pic.leetcode-cn.com/992f95361c37ad06deadb6f14a9970d0184fd47330365400dd1d6f7be239e0ff-image.png)


```
class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    // Make a copy of nums1.
    int [] nums1_copy = new int[m];
    System.arraycopy(nums1, 0, nums1_copy, 0, m);

    // Two get pointers for nums1_copy and nums2.
    int p1 = 0;
    int p2 = 0;

    // Set pointer for nums1
    int p = 0;

    // Compare elements from nums1_copy and nums2
    // and add the smallest one into nums1.
    while ((p1 < m) && (p2 < n))
      nums1[p++] = (nums1_copy[p1] < nums2[p2]) ? nums1_copy[p1++] : nums2[p2++];

    // if there are still elements to add
    if (p1 < m)
      System.arraycopy(nums1_copy, p1, nums1, p1 + p2, m + n - p1 - p2);
    if (p2 < n)
      System.arraycopy(nums2, p2, nums1, p1 + p2, m + n - p1 - p2);
  }
}
```
**复杂度分析：**
- 时间复杂度：O(n+m)。
- 空间复杂度：O(m)。

### 3.双指针-从后向前
**思路：**

![](https://pic.leetcode-cn.com/358c5531639dff237d3a5b7d51d101f652d6409ff6a24f4ca601a277a4b859c5-image.png)

```
class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    // two get pointers for nums1 and nums2
    int p1 = m - 1;
    int p2 = n - 1;
    // set pointer for nums1
    int p = m + n - 1;

    // while there are still elements to compare
    while ((p1 >= 0) && (p2 >= 0))
      // compare two elements from nums1 and nums2
      // and add the largest one in nums1
      nums1[p--] = (nums1[p1] < nums2[p2]) ? nums2[p2--] : nums1[p1--];

    // add missing elements from nums2
    System.arraycopy(nums2, 0, nums1, 0, p2 + 1);
  }
}
```
**复杂度分析：**
- 时间复杂度：O(n+m)。
- 空间复杂度：O(1)。

## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/merge-sorted-array/solution/he-bing-liang-ge-you-xu-shu-zu-by-leetcode/)***
