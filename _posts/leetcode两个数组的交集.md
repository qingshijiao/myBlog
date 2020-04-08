---
title: 349.两个数组的交集 (Intersection of Two Arrays)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [349\. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

Difficulty: **简单**


给定两个数组，编写一个函数来计算它们的交集。

**示例 1:**

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

**示例 2:**

```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```

**说明:**

*   输出结果中的每个元素一定是唯一的。
*   我们可以不考虑输出结果的顺序。


#### Solution

Language: **Java**

```java
​class Solution {
   public int[] intersection(int[] nums1, int[] nums2) {
        // 作为临时的交集
        int[] container = nums1.length > nums2.length ?
                        new int[nums1.length] : new int[nums2.length];

        boolean[] appeared = new boolean[2020];
        for (int i = 0; i < nums1.length; i++) {
            appeared[nums1[i]] = true;      // 标记nums1的各个元素为出现过
        }

        int len = 0;                          // 定位指针
        for (int i = 0; i < nums2.length; i++) {
            if (appeared[nums2[i]] == true) {
                container[len++] = nums2[i];
                appeared[nums2[i]] = false; //标记其状态为使用过
            }
        }

        int[] resArr = new int[len];          //len-0 == 为交集的元素个数
        for (int i = 0; i < len; i++) {
            resArr[i] = container[i];
        }
        return resArr;

    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/intersection-of-two-arrays/)***
