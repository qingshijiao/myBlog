---
title: 63. 不同路径 II（Unique Paths II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？


![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

网格中的障碍物和空位置分别用 1 和 0 来表示。

**说明：** m 和 n 的值均不超过 100。

示例 1:
```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```


# 题解

## 官方题解
### 1.动态规划
**思路：**

![](https://pic.leetcode-cn.com/8aafa0b433830e1c1e26e5478ffed7d9c3f1f46ab0f666bdc95380a81a0fd59d-image.png)
![](https://pic.leetcode-cn.com/234e10fdf3fdeac41f9eb201e011cc8dff264b255cd62a856053b0d966a77e7d-image.png)
![](https://pic.leetcode-cn.com/a0de11361998341eb5228f171be1b6e900dad72229c1ca8bd80afd68011e307e-image.png)


```
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {

        int R = obstacleGrid.length;
        int C = obstacleGrid[0].length;

        // If the starting cell has an obstacle, then simply return as there would be
        // no paths to the destination.
        if (obstacleGrid[0][0] == 1) {
            return 0;
        }

        // Number of ways of reaching the starting cell = 1.
        obstacleGrid[0][0] = 1;

        // Filling the values for the first column
        for (int i = 1; i < R; i++) {
            obstacleGrid[i][0] = (obstacleGrid[i][0] == 0 && obstacleGrid[i - 1][0] == 1) ? 1 : 0;
        }

        // Filling the values for the first row
        for (int i = 1; i < C; i++) {
            obstacleGrid[0][i] = (obstacleGrid[0][i] == 0 && obstacleGrid[0][i - 1] == 1) ? 1 : 0;
        }

        // Starting from cell(1,1) fill up the values
        // No. of ways of reaching cell[i][j] = cell[i - 1][j] + cell[i][j - 1]
        // i.e. From above and left.
        for (int i = 1; i < R; i++) {
            for (int j = 1; j < C; j++) {
                if (obstacleGrid[i][j] == 0) {
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1];
                } else {
                    obstacleGrid[i][j] = 0;
                }
            }
        }

        // Return value stored in rightmost bottommost cell. That is the destination.
        return obstacleGrid[R - 1][C - 1];
    }
}

```

**复杂度分析：**
- 时间复杂度： O(M×N) 。长方形网格的大小是 M×N，而访问每个格点恰好一次。
- 空间复杂度：O(1)，我们利用 obstacleGrid 作为 DP 数组，因此不需要额外的空间。



## 其他题解
### 1.加边界
**思路：** 思路是给左面和上面各加一个障碍边，这样不用对边界做判断。
`dp[n] 做边界`

```
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid[0][0] == 1){
            return 0;
        }
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[] dp = new int[n + 1];
        Arrays.fill(dp, 0);
        dp[0] = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (obstacleGrid[i][j] == 0){
                    if (j == 0) {
                        dp[j] = dp[n] + dp[j];
                    } else {
                        dp[j] = dp[j - 1] + dp[j];
                    }
                } else {
                    dp[j] = 0;
                }
            }
            System.out.println(Arrays.toString(dp));
        }
        return dp[n - 1];
    }
}
```

m, n 和 java 表示的含义相反
```
# python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m, n = len(obstacleGrid[0]), len(obstacleGrid)
        dp = [1] + [0]*m
        for i in range(0, n):
            for j in range(0, m):
                dp[j] = 0 if obstacleGrid[i][j] else dp[j]+dp[j-1]
        return dp[-2]

```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/unique-paths-ii/solution/bu-tong-lu-jing-ii-by-leetcode/)
[yslucas](https://leetcode-cn.com/problems/unique-paths-ii/solution/python3liu-xing-jian-ji-dai-ma-shi-jian-kong-jian-/)***
