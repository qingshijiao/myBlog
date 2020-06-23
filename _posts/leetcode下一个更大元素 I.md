---
title: 496. 下一个更大元素 I（Next Greater Element I）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [496\. Next Greater Element I](https://leetcode-cn.com/problems/next-greater-element-i/)

Difficulty: **简单**


给定两个 **没有重复元素** 的数组 `nums1` 和 `nums2` ，其中`nums1` 是 `nums2` 的子集。找到 `nums1` 中每个元素在 `nums2` 中的下一个比其大的值。

`nums1` 中数字 **x** 的下一个更大元素是指 **x** 在 `nums2` 中对应位置的右边的第一个比 **x **大的元素。如果不存在，对应位置输出 -1 。

**示例 1:**

```
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
    对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
    对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
```

**示例 2:**

```
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于 num1 中的数字 2 ，第二个数组中的下一个较大数字是 3 。
    对于 num1 中的数字 4 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
```

**提示：**

1.  `nums1`和`nums2`中所有元素是唯一的。
2.  `nums1`和`nums2` 的数组大小都不超过1000。


#### Solution

Language: **Java**

```java
​class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        if(nums1.length == 0){
            return nums1;
        }
        int max = nums2[0];
        int min = nums2[0];

        for(int val : nums2){
            if(max < val){
                max = val;
            }
            if(min > val){
                min = val;
            }
        }

        int[] buf = new int[max - min + 1];

        buf[nums2[nums2.length - 1] - min] = -1;

        for(int j = nums2.length - 2 ; j >=0; j--){
            int cur = nums2[j];
            int nxt = nums2[j + 1];

            while(cur > nxt && nxt != -1){
                nxt = buf[nxt - min];
            }
            buf[cur - min] = nxt;

        }

        int[] res = new int[nums1.length];

        for(int i = 0; i < nums1.length; i++){
            res[i] = buf[nums1[i] - min];
        }
        return res;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/next-greater-element-i/submissions/)***
