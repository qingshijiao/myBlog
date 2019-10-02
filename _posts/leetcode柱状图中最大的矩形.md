---
title: 84.柱状图中最大的矩形(Largest Rectangle in Histogram)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)

图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

示例:
```
输入: [2,1,5,6,2,3]
输出: 10
```


# 题解

## 官方题解
### 1.暴力法
**思想：** 首先，我们可以想到，两个柱子间矩形的高由它们之间最矮的柱子决定。如下图所示：

![](https://pic.leetcode-cn.com/0239df28a3a9d97a96c773a4b5babc59cf55219332f815eda3fc240a7d530cda-image.png)

因此，我们可以考虑所有两两柱子之间形成的矩形面积，该矩形的高为它们之间最矮柱子的高度，宽为它们之间的距离，这样可以找到所要求的最大面积的矩形。
```
public class Solution {
   public int largestRectangleArea(int[] heights) {
       int maxarea = 0;
       for (int i = 0; i < heights.length; i++) {
           for (int j = i; j < heights.length; j++) {
               int minheight = Integer.MAX_VALUE;
               for (int k = i; k <= j; k++)
                   minheight = Math.min(minheight, heights[k]);
               maxarea = Math.max(maxarea, minheight * (j - i + 1));
           }
       }
       return maxarea;
   }
}
```
**复杂度分析：**
- 时间复杂度：O(n^3)。我们需要使用 O(n) 的时间找到 O(n^2) 枚举出来的所有柱子对之间的最矮柱子
- 空间复杂度: O(1)。 只需要常数空间的额外变量

### 2.优化的暴力法
**思想：** 我们可以基于方法 1 进行一点点修改来优化算法。我们可以用前一对柱子之间的最低高度来求出当前柱子对间的最低高度。

用数学语言来表达，minheight=min(minheight,heights(j)) ，其中，heights(j) 是第 j 个柱子的高度。

```
public class Solution {
   public int largestRectangleArea(int[] heights) {
       int maxarea = 0;
       for (int i = 0; i < heights.length; i++) {
           int minheight = Integer.MAX_VALUE;
           for (int j = i; j < heights.length; j++) {
               minheight = Math.min(minheight, heights[j]);
               maxarea = Math.max(maxarea, minheight * (j - i + 1));
           }
       }
       return maxarea;
   }
}
```
**复杂度分析：**
- 时间复杂度：O(n^2)。 需要枚举所有可能的柱子对。
- 空间复杂度：O(1)。不需要额外的空间。


### 3.分治
**思想：** 通过观察，可以发现，最大面积矩形存在于以下几种情况：

- 确定了最矮柱子以后，矩形的宽尽可能往两边延伸。
- 在最矮柱子左边的最大面积矩形（子问题）。
- 在最矮柱子右边的最大面积矩形（子问题）。

![](https://pic.leetcode-cn.com/2013f70b237a16bcf8bae8f5873669b8b21d5300b2ed254adbddd2b9b577f02b-image.png)


```
public class Solution {
    public int calculateArea(int[] heights, int start, int end) {
        if (start > end)
            return 0;
        int minindex = start;
        for (int i = start; i <= end; i++)
            if (heights[minindex] > heights[i])
                minindex = i;
        return Math.max(heights[minindex] * (end - start + 1), Math.max(calculateArea(heights, start, minindex - 1), calculateArea(heights, minindex + 1, end)));
    }
    public int largestRectangleArea(int[] heights) {
        return calculateArea(heights, 0, heights.length - 1);
    }
}
```
**复杂度分析：**
- 时间复杂度：
  - 平均开销：O(nlogn)
  - 最坏情况：O(n^2)。如果数组中的数字是有序的，分治算法将没有任何优化效果。
- 空间复杂度：O(n)。最坏情况下递归需要 O(n) 的空间。


### 4.优化的分治
**思想：** 可以观察到，方法 3 中大的问题被分解成更小的子问题来求解，所以分治方法会有一定程度的优化。但是如果数组本身是升序或者降序的，将没有优化作用，原因是每次我们都需要在一个很大的 O(n) 级别的数组里找最小值。因此，最坏情况下总的时间复杂度变成了 O(n^2)。我们可以用线段树代替遍历来找到区间最小值。单词查询复杂度就变成了O(logn) 。

[代码](https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28941/segment-tree-solution-just-another-idea-onlogn-solution)

**复杂度分析：**
- 时间复杂度：O(nlogn) 。 对于长度为 n 的查询，线段树需要 logn 的时间。
- 空间复杂度：O(n)O(n)。这是线段树的空间开销。


### 5.栈
**思想：**

![](https://pic.leetcode-cn.com/eecfe2ec7c58bc2271384f6389731c655309f34cfd7dd2e91f6e6d0edf243430-image.png)
![](https://pic.leetcode-cn.com/12ccce1435f76e3ac852b574391430d01b8db7c8ef263cbe9d0f62759f7f0fdd-image.png)
![](https://pic.leetcode-cn.com/8b67a39213543ec0a0920ff8f98fad7cbc54950c92853231b64eecedde03ccc4-image.png)

```
public class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack < Integer > stack = new Stack < > ();
        stack.push(-1);
        int maxarea = 0;
        for (int i = 0; i < heights.length; ++i) {
            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i])
                maxarea = Math.max(maxarea, heights[stack.pop()] * (i - stack.peek() - 1));
            stack.push(i);
        }
        while (stack.peek() != -1)
            maxarea = Math.max(maxarea, heights[stack.pop()] * (heights.length - stack.peek() -1));
        return maxarea;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n)。 n 个数字每个会被压栈弹栈各一次。
- 空间复杂度： O(n)。用来存放栈中元素。


## 其他题解
### 1.分治
**思想：**

```
class Solution {
    public int largestRectangleArea(int[] heights) {

        int len= heights.length;
        if(len==0)
            return 0;
        return maxArea(heights, 0, len-1);
    }


    private int maxArea(int[] h, int left, int right) {
        if (left==right)
            return h[right];
        int min= left;
        boolean sorted= true;
        for (int i= left+1; i<=right; i++) {
            if (h[i]<h[i-1])
                sorted= false;
            if (h[i]<h[min])
                min= i;
        }
        if (sorted) {
            int max=0;
            for (int i=left; i<=right; i++)
                  max= Math.max(max, h[i]*(right-i+1));
            return max;
        }
        int l= (min>left)? maxArea(h, left, min-1): 0;
        int r= (min<right)? maxArea(h, min+1, right): 0;
        return Math.max(Math.max(l, r), h[min]*(right-left+1));
    }

}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/solution/zhu-zhuang-tu-zhong-zui-da-de-ju-xing-by-leetcode/)***
