---
title: 363.矩形区域不超过 K 的最大数值和 (Max Sum of Rectangle No Larger Than K)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [363\. 矩形区域不超过 K 的最大数值和](https://leetcode-cn.com/problems/max-sum-of-rectangle-no-larger-than-k/)

Difficulty: **困难**


给定一个非空二维矩阵 _matrix _和一个整数 _k_，找到这个矩阵内部不大于 _k_ 的最大矩形和。

**示例:**

```
输入: matrix = [[1,0,1],[0,-2,3]], k = 2
输出: 2
解释: 矩形区域 [[0, 1], [-2, 3]] 的数值和是 2，且 2 是不超过 k 的最大数字（k = 2）。
```

**说明：**

1.  矩阵内的矩形区域面积必须大于 0。
2.  如果行数远大于列数，你将如何解答呢？


#### Solution

Language: **Java**

```java
​class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        if(matrix == null || matrix[0] == null) {
            return 0;
        }
        // 行列
        int row = matrix.length;
        int col = matrix[0].length;
        // 最大面积记录
        int  maxArea = Integer.MIN_VALUE;
        // 列压缩
        for(int i = 0; i < col; i++) {
            // 记录压缩历史列
            int[] compressCol = new int[row];
            // 向右压缩
            for(int j = i; j < col; j++) {
                int sum = 0;
                int tempArea = Integer.MIN_VALUE;
                for(int r = 0; r < row; r++) {
                    compressCol[r] += matrix[r][j];
                    if(sum < 0)
                        sum = 0;
                    sum+= compressCol[r];
                    tempArea = Math.max(tempArea, sum);
                }

                    if(tempArea <= k) {
                        maxArea = Math.max(maxArea, tempArea);
                    } else {
                        tempArea = Integer.MIN_VALUE;
                        for(int m = 0; m < row; m++) {
                            sum = 0;
                            for(int n = m; n < row; n++) {
                                sum += compressCol[n];
                                if(sum <= k)
                                    tempArea = Math.max(tempArea, sum);
                            }
                        }
                        maxArea = Math.max(maxArea, tempArea);
                    }
                    //目标变成找到k，存在k时很快，不存在时退化到正常速度
                    if(maxArea == k)
                        return k;
                }
            }
            return maxArea;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/max-sum-of-rectangle-no-larger-than-k/submissions/)***
