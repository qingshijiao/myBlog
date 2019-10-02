---
title: 85.最大矩形(Maximal Rectangle)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

示例:
```
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```


# 题解

## 官方题解
### 1.暴力法
**思想：** 最原始地，我们可以列举每个可能的矩形。这可以通过遍历所有的(x1, y1) (x2, y2) 坐标，并以它们为对角顶点来完成。该方法过慢，不足以通过所有测试用例。

![01.png](https://i.loli.net/2019/10/02/f2slx5LCTHRtkAb.png)


### 2.动态规划 - 使用柱状图的优化暴力方法
**思想：** 我们可以以常数时间计算出在给定的坐标结束的矩形的最大宽度。我们可以通过记录每一行中每一个方块连续的“1”的数量来实现这一点。每遍历完一行，就更新该点的最大可能宽度。通过以下代码即可实现。
`row[i] = row[i - 1] + 1 if row[i] == '1'.`

![](https://pic.leetcode-cn.com/ab17561e25fee6e943ebe1a0678480f7fc75cef29008a4ed470067c51bd0831b-image.png)


![](https://pic.leetcode-cn.com/bb40b26be66a20c49bf797b908fd00589c1df90c27c1e4789323e1d0a983b8e6-image.png)
![](https://pic.leetcode-cn.com/14a6767d8e49b00e351b6e052143dfa826148c22a7e13c3a05c55ea401d05f18-image.png)
![](https://pic.leetcode-cn.com/d553e8ea8ba5f36a01dadd3530a31cadc2a98aa5b7d8f591fcb36b6c2604784a-image.png)

```
class Solution {
    public int maximalRectangle(char[][] matrix) {

        if (matrix.length == 0) return 0;
        int maxarea = 0;
        int[][] dp = new int[matrix.length][matrix[0].length];

        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                if (matrix[i][j] == '1'){

                    // compute the maximum width and update dp with it
                    dp[i][j] = j == 0? 1 : dp[i][j-1] + 1;

                    int width = dp[i][j];

                    // compute the maximum area rectangle with a lower right corner at [i, j]
                    for(int k = i; k >= 0; k--){
                        width = Math.min(width, dp[k][j]);
                        maxarea = Math.max(maxarea, width * (i - k + 1));
                    }
                }
            }
        } return maxarea;
    }
}
```
![02.png](https://i.loli.net/2019/10/02/6AGXavoKekY3izy.png)


### 3.使用柱状图 - 栈
**思想：** 在上一方法中我们讨论了将输入拆分成一系列的柱状图，每个柱状图代表一列的子结构。为了计算长方形的最大面积，我们仅仅需要计算每个柱状图中的最大面积并找到全局最大值（注意后面的解法对每一行而非列建立了柱状图，两者思想一致）。


```
class Solution {

    // Get the maximum area in a histogram given its heights
    public int leetcode84(int[] heights) {
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

    public int maximalRectangle(char[][] matrix) {

        if (matrix.length == 0) return 0;
        int maxarea = 0;
        int[] dp = new int[matrix[0].length];

        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {

                // update the state of this row's histogram using the last row's histogram
                // by keeping track of the number of consecutive ones

                dp[j] = matrix[i][j] == '1' ? dp[j] + 1 : 0;
            }
            // update maxarea with the maximum area from this row's histogram
            maxarea = Math.max(maxarea, leetcode84(dp));
        } return maxarea;
    }
}
```
**复杂度分析：**
- 时间复杂度：时间复杂度 : O(NM)。对每一行运行 力扣 84 需要 M (每行长度) 时间，运行了 N 次，共计 O(NM)。
- 空间复杂度：O(M)。我们声明了长度等于列数的数组，用于存储每一行的宽度。


### 4.动态规划 - 每个点的最大高度
**思想：** 想象一个算法，对于每个点我们会通过以下步骤计算一个矩形：

- 不断向上方遍历，直到遇到“0”，以此找到矩形的最大高度。
- 向左右两边扩展，直到无法容纳矩形最大高度。

![](https://pic.leetcode-cn.com/7afdf3b28c24af7ac7a9d97463823ebfe1e43580c443cfb8482ad9b02723f70f-image.png)
![](https://pic.leetcode-cn.com/e41e88f92dcb5597a1dd336e0ab713b4c2e3281e99d144e58bbffc7c89836716-image.png)
![](https://pic.leetcode-cn.com/587924f9696b0ea30e056daa03520fc400c7688ba26be2acab4cd9775d76e385-image.png)

```
class Solution {

    public int maximalRectangle(char[][] matrix) {
        if(matrix.length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;

        int[] left = new int[n]; // initialize left as the leftmost boundary possible
        int[] right = new int[n];
        int[] height = new int[n];

        Arrays.fill(right, n); // initialize right as the rightmost boundary possible

        int maxarea = 0;
        for(int i = 0; i < m; i++) {
            int cur_left = 0, cur_right = n;
            // update height
            for(int j = 0; j < n; j++) {
                if(matrix[i][j] == '1') height[j]++;
                else height[j] = 0;
            }
            // update left
            for(int j=0; j<n; j++) {
                if(matrix[i][j]=='1') left[j]=Math.max(left[j],cur_left);
                else {left[j]=0; cur_left=j+1;}
            }
            // update right
            for(int j = n - 1; j >= 0; j--) {
                if(matrix[i][j] == '1') right[j] = Math.min(right[j], cur_right);
                else {right[j] = n; cur_right = j;}
            }
            // update area
            for(int j = 0; j < n; j++) {
                maxarea = Math.max(maxarea, (right[j] - left[j]) * height[j]);
            }
        return maxarea;
    }
}
```


**复杂度分析：**
- 时间复杂度：O(NM)。每次对于N的迭代我们会对M迭代常数次。
- 空间复杂度： O(M)， M 是我们保留的额外数组的长度。


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/maximal-rectangle/solution/zui-da-ju-xing-by-leetcode/)***
