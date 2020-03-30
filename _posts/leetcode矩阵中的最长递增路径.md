---
title: 329.矩阵中的最长递增路径 (Longest Increasing Path in a Matrix)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [329\. 矩阵中的最长递增路径](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)

Difficulty: **困难**


给定一个整数矩阵，找出最长递增路径的长度。

对于每个单元格，你可以往上，下，左，右四个方向移动。 你不能在对角线方向上移动或移动到边界外（即不允许环绕）。

**示例 1:**

```
输入: nums =
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
]
输出: 4
解释: 最长递增路径为 [1, 2, 6, 9]。
```

**示例 2:**

```
输入: nums =
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
]
输出: 4
解释: 最长递增路径是 [3, 4, 5, 6]。注意不允许在对角线方向上移动。
```


#### Solution1 - 记忆化深度搜索

Language: **Java**
time:O(mn) space:O(mn)
```java
​// DFS + Memoization Solution
// Accepted and Recommended
public class Solution {
    private static final int[][] dirs = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int m, n;

    public int longestIncreasingPath(int[][] matrix) {
        if (matrix.length == 0) return 0;
        m = matrix.length; n = matrix[0].length;
        int[][] cache = new int[m][n];
        int ans = 0;
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                ans = Math.max(ans, dfs(matrix, i, j, cache));
        return ans;
    }

    private int dfs(int[][] matrix, int i, int j, int[][] cache) {
        if (cache[i][j] != 0) return cache[i][j];
        for (int[] d : dirs) {
            int x = i + d[0], y = j + d[1];
            if (0 <= x && x < m && 0 <= y && y < n && matrix[x][y] > matrix[i][j])
                cache[i][j] = Math.max(cache[i][j], dfs(matrix, x, y, cache));
        }
        return ++cache[i][j];
    }
}
```

```java
class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int[][] cache = new int[matrix.length][matrix[0].length];
        int max = 0;
        for (int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {
                int len = dfs(matrix, i, j, cache, -1);
                max = Math.max(max, len);
            }
        }
        return max;
    }
    private int dfs(int[][] matrix,int i, int j, int[][] cache, int pre){
        if (i < 0 || j < 0 || i >= matrix.length || j >= matrix[0].length || matrix[i][j] <= pre) {
            return 0;
        }
        if (cache[i][j] > 0) {
            return cache[i][j];
        } else {
            int cur = matrix[i][j];
            int tempMax = 0;
            tempMax = Math.max(tempMax, dfs(matrix, i - 1 , j, cache, cur));
            tempMax = Math.max(tempMax, dfs(matrix, i, j - 1, cache, cur));
            tempMax = Math.max(tempMax, dfs(matrix, i, j + 1, cache, cur));
            tempMax = Math.max(tempMax, dfs(matrix, i + 1, j, cache, cur));
            tempMax++;
            cache[i][j] += tempMax;
            return tempMax;
        }
    }
}
```

#### Solution2 - “剥洋葱”（动态规划）

Language: **Java**
time:O(mn) space:O(mn)
```java
​// Topological Sort Based Solution
// An Alternative Solution
public class Solution {
    private static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int m, n;
    public int longestIncreasingPath(int[][] grid) {
        int m = grid.length;
        if (m == 0) return 0;
        int n = grid[0].length;
        // padding the matrix with zero as boundaries
        // assuming all positive integer, otherwise use INT_MIN as boundaries
        int[][] matrix = new int[m + 2][n + 2];
        for (int i = 0; i < m; ++i)
            System.arraycopy(grid[i], 0, matrix[i + 1], 1, n);

        // calculate outdegrees
        int[][] outdegree = new int[m + 2][n + 2];
        for (int i = 1; i <= m; ++i)
            for (int j = 1; j <= n; ++j)
                for (int[] d: dir)
                    if (matrix[i][j] < matrix[i + d[0]][j + d[1]])
                        outdegree[i][j]++;

        // find leaves who have zero out degree as the initial level
        n += 2;
        m += 2;
        List<int[]> leaves = new ArrayList<>();
        for (int i = 1; i < m - 1; ++i)
            for (int j = 1; j < n - 1; ++j)
                if (outdegree[i][j] == 0) leaves.add(new int[]{i, j});

        // remove leaves level by level in topological order
        int height = 0;
        while (!leaves.isEmpty()) {
            height++;
            List<int[]> newLeaves = new ArrayList<>();
            for (int[] node : leaves) {
                for (int[] d:dir) {
                    int x = node[0] + d[0], y = node[1] + d[1];
                    if (matrix[node[0]][node[1]] > matrix[x][y])
                        if (--outdegree[x][y] == 0)
                            newLeaves.add(new int[]{x, y});
                }
            }
            leaves = newLeaves;
        }
        return height;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/solution/ju-zhen-zhong-de-zui-chang-di-zeng-lu-jing-by-leet/)***
