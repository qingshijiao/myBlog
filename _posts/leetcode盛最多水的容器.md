---
title: 11.盛最多水的容器（Container With Most Water）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

**说明：** 你不能倾斜容器，且 n 的值至少为 2。
![](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)


图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

 

示例:
> 输入: [1,8,6,2,5,4,8,3,7]
> 输出: 49


# 题解
> 如题意，垂直的两条线段将会与坐标轴构成一个矩形区域，较短线段的长度将会作为矩形区域的宽度，两线间距将会作为矩形区域的长度，而我们必须最大化该矩形区域的面积。

## 官方题解
### 1.暴力法
**思路：** 在这种情况下，我们将简单地考虑每对可能出现的线段组合并找出这些情况之下的最大面积。

```
public class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0;
        for (int i = 0; i < height.length; i++)
            for (int j = i + 1; j < height.length; j++)
                maxarea = Math.max(maxarea, Math.min(height[i], height[j]) * (j - i));
        return maxarea;
    }
}
```

> 复杂度分析
> - 时间复杂度：O(n^2)
> - 空间复杂度：O(1)

### 2.双指针法
**思想：** 定义两个指针，分别指向头和尾，比较两个长度，长度短的向长度长的移动，每次记录下最大面积。两线段之间形成的区域总是会受到其中较短那条长度的限制。此外，两线段距离越远，得到的面积就越大。
**算法：** 现在，为了使面积最大化，我们需要考虑更长的两条线段之间的区域。如果我们试图将指向较长线段的指针向内侧移动，**矩形区域的面积将受限于较短的线段而不会获得任何增加**。但是，在同样的条件下，移动指向较短线段的指针尽管造成了矩形宽度的减小，**但却可能会有助于面积的增大**。因为移动较短线段的指针会得到一条相对较长的线段，这可以克服由宽度减小而引起的面积减小。
> **问：** 会不会忽略了最大值？
> **答：** 不会。因为面积是由最短长度和宽度决定的。假设最短长度固定，移动最长长度，宽度减小，但是由于是 面积 = 最短长度 * 宽度，面积还是减小了，我们舍弃的就是这部分面积减小的无效数对。
```
public class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0, l = 0, r = height.length - 1;
        while (l < r) {
            maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return maxarea;
    }
}
```

> 复杂度分析
> - 时间复杂度：O(n)
> - 空间复杂度：O(1)


## 其他题解
暂无

---
***参考：
[领扣](https://leetcode-cn.com/problems/container-with-most-water/solution/sheng-zui-duo-shui-de-rong-qi-by-leetcode/)***
