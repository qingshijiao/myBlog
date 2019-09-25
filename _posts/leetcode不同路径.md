---
title: 62. 不同路径（Unique Paths）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

例如，上图是一个7 x 3 的网格。有多少可能的路径？

**说明：** m 和 n 的值均不超过 100。

示例 1:
```
输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
```
示例 2:
```
输入: m = 7, n = 3
输出: 28
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.排列组合
**思路：**
因为机器到底右下角，向下几步，向右几步都是固定的，

比如，m=3, n=2，我们只要向下 1 步，向右 2 步就一定能到达终点。

所以有 C^m+n−2^m−1
​
```
class Solution {
    public int uniquePaths(int m, int n) {
        int N = n + m - 2;
        int k = m - 1;
        long res = 1;
        for (int i = 1; i <= k; i++)
            res = res * (N - k + i) / i;
        return (int) res;
    }

}

```
**复杂度分析：**
- 时间复杂度：O(n)
- 空间复杂度：O(1)

### 2.递归
**思路：**
求 ( 0 , 0 ) 点到（ m - 1 , n - 1） 点的走法。
```
class Solution {
    public int uniquePaths(int m, int n) {
        HashMap<String, Integer> visited = new HashMap<>();
        return getAns(m - 1, n - 1, 0, 0, 0, visited);

    }
    private int getAns(int x, int y, int m, int n, int num, HashMap<String, Integer> visited) {
        if (x == m && y == n) {
            return 1;
        }
        int n1 = 0;
        int n2 = 0;
        String key = x - 1 + "@" + y;
        //判断当前点是否已经求过了
        if (!visited.containsKey(key)) {
            if (x - 1 >= m) {
                n1 = getAns(x - 1, y, m, n, num, visited);
            }
        } else {
            n1 = visited.get(key);
        }
        key = x + "@" + (y - 1);
        if (!visited.containsKey(key)) {
            if (y - 1 >= n) {
                n2 = getAns(x, y - 1, m, n, num, visited);
            }
        } else {
            n2 = visited.get(key);
        }
        //将当前点加入 visited 中
        key = x + "@" + y;
        visited.put(key, n1+n2);
        return n1 + n2;
    }

}

```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：

### 3.动态规划
**思路：**
可以用二维数组储存，也可以用一维数组储存（存储前一行/列信息）
![](https://i.loli.net/2019/09/25/Lfx9nogeA3h6rSX.png)
​
```
class Solution {
    public int uniquePaths(int m, int n) {
        int[] memo = new int[n];

        Arrays.fill(memo, 1);

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                memo[j] += memo[j - 1];
            }
        }

        return memo[n - 1];
    }

}
```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/unique-paths/submissions/)
[windliang](https://leetcode-cn.com/problems/unique-paths/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-20/)
[powcai](https://leetcode-cn.com/problems/unique-paths/solution/dong-tai-gui-hua-by-powcai-2/)
[BiYu2019](https://leetcode-cn.com/problems/unique-paths/solution/xiao-xue-ti-java-by-biyu_leetcode/)***
