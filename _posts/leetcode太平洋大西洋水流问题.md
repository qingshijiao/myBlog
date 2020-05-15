---
title: 417.太平洋大西洋水流问题 (Pacific Atlantic Water Flow)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [417\. 太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

Difficulty: **中等**


给定一个 `m x n` 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。

规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。

请找出那些水流既可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。

**提示：**

1.  输出坐标的顺序不重要
2.  _m_ 和 _n_ 都小于150

**示例：**

```
给定下面的 5x5 矩阵:

  太平洋 ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * 大西洋

返回:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元).
```


#### Solution

Language: **Java**

```java
​class Solution {
    private static final int[][] dirs = {
            {-1, 0}, {1, 0}, {0, -1}, {0, 1}
    };

    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        if (matrix == null || matrix.length == 0)
            return new ArrayList<>();
        int m = matrix.length, n = matrix[0].length;

        boolean[][] isPO = new boolean[m][n];
        boolean[][] isAO = new boolean[m][n];

        for (int i = 0; i < n; i++) {
            dfs(matrix[0][i], 0, i, isPO, matrix);
            dfs(matrix[m - 1][i], m - 1, i, isAO, matrix);
        }
        for (int i = 0; i < m - 1; i++) {
            dfs(matrix[i + 1][0], i + 1, 0, isPO, matrix);
            dfs(matrix[i][n - 1], i, n - 1, isAO, matrix);
        }

        List<List<Integer>> ret = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (isPO[i][j] && isAO[i][j]) {
                    ret.add(Arrays.asList(i, j));
                }
            }
        }
        return ret;
    }

    private void dfs(int preVal, int x, int y, boolean[][] flag, int[][] matrix) {
        if (x < 0 || x >= matrix.length || y < 0 || y >= matrix[0].length || flag[x][y] || preVal > matrix[x][y]) {
            return;
        }
        flag[x][y] = true;
        for (int[] dir : dirs) {
            dfs(matrix[x][y], x + dir[0], y + dir[1], flag, matrix);
        }
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/submissions/)***
