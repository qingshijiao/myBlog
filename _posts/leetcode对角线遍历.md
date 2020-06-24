---
title: 498. 对角线遍历（Diagonal Traverse）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [498\. 对角线遍历](https://leetcode-cn.com/problems/diagonal-traverse/)

Difficulty: **中等**


给定一个含有 M x N 个元素的矩阵（M 行，N 列），请以对角线遍历的顺序返回这个矩阵中的所有元素，对角线遍历如下图所示。

**示例:**

```
输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

输出:  [1,2,4,7,5,3,6,8,9]

解释:

```

**说明:**

1.  给定矩阵中的元素总数不会超过 100000 。


#### Solution

Language: **Java**

```java
​class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if(matrix.length == 0)
            return new int[] {};
        if(matrix.length == 1) 
            return matrix[0];
        
        int[] r = new int[matrix.length*matrix[0].length];
        r[0] = (matrix[0][0]);
        traverse(matrix, 0, 0, r, 0);
        return r;
    }

    public void traverse(int[][] matrix, int i, int j, int[] r, int cur) {  
        if(i == 0) {
            if(j != matrix[0].length-1)
                r[++cur] = matrix[i][++j];
            else
                r[++cur] = matrix[++i][j];
            while(j > 0 && i < matrix.length-1)
                r[++cur] = matrix[++i][--j];
        }
        else if(i == matrix.length-1) {
            if(j == matrix[0].length-1)
                return;
            else
                r[++cur] = matrix[i][++j];
            while(i > 0 && j < matrix[0].length-1)
                r[++cur] = matrix[--i][++j];
        }
        else if(j == 0) {
            if(i != matrix.length-1)
                r[++cur] = matrix[++i][j];
            else
                r[++cur] = matrix[i][++j];
            while(i > 0 && j < matrix[0].length-1)
                r[++cur] = matrix[--i][++j];
        }
        else {
            if(i == matrix.length-1)
                return;
            else
                r[++cur] = matrix[++i][j];
            while(j > 0 && i < matrix.length-1)
                r[++cur] = matrix[++i][--j];
        }
        traverse(matrix, i, j, r, cur);
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/diagonal-traverse/)***
