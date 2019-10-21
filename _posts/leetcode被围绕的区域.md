---
title: 130.被围绕的区域（Surrounded Regions）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二维的矩阵，包含 'X' 和 'O'（字母 O）。

找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

示例:
```
X X X X
X O O X
X X O X
X O X X

运行你的函数后，矩阵变为：

X X X X
X X X X
X X X X
X O X X
```

**解释:**

被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。



# 题解

## 官方题解
暂无

## 其他题解
从边界出发吧，先把边界上和 O 连通点找到, 把这些变成 B,然后遍历整个 board 把 O 变成 X, 把 B 变成 O

![](https://pic.leetcode-cn.com/f6cc252beb78212f68d55136cf6093419c3a07cb2f2ccbcc53f8fc064d27708a-tmp.png)

### 1.DFS
**思路：**

```
class Solution {
    int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public void solve(char[][] board) {
        if (board == null || board.length == 0 || board[0] == null || board[0].length == 0) return;
        int row = board.length;
        int col = board[0].length;
        for (int j = 0; j < col; j++) {
            // 第一行
            if (board[0][j] == 'O') dfs(0, j, board, row, col);
            // 最后一行
            if (board[row - 1][j] == 'O') dfs(row - 1, j, board, row, col);
        }

        for (int i = 0; i < row; i++) {
            // 第一列
            if (board[i][0] == 'O') dfs(i, 0, board, row, col);
            // 最后一列
            if (board[i][col - 1] == 'O') dfs(i, col - 1, board, row, col);
        }

        // 转变
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == 'B') board[i][j] = 'O';
            }
        }

    }

    private void dfs(int i, int j, char[][] board, int row, int col) {
        board[i][j] = 'B';
        for (int[] dir : dirs) {
            int tmp_i = dir[0] + i;
            int tmp_j = dir[1] + j;
            if (tmp_i < 0 || tmp_i >= row || tmp_j < 0 || tmp_j >= col || board[tmp_i][tmp_j] != 'O') continue;
            dfs(tmp_i, tmp_j, board, row, col);
        }
    }
}
```

### 2.BFS
**思路：**

```
class Solution {
    int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    private static class Point {
        int x, y;

        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public void solve(char[][] board) {
        if (board == null || board.length == 0 || board[0] == null || board[0].length == 0) return;
        int row = board.length;
        int col = board[0].length;
        for (int j = 0; j < col; j++) {
            // 第一行
            if (board[0][j] == 'O') bfs(0, j, board, row, col);
            // 最后一行
            if (board[row - 1][j] == 'O') bfs(row - 1, j, board, row, col);
        }

        for (int i = 0; i < row; i++) {
            // 第一列
            if (board[i][0] == 'O') bfs(i, 0, board, row, col);
            // 最后一列
            if (board[i][col - 1] == 'O') bfs(i, col - 1, board, row, col);
        }

        // 转变
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == 'B') board[i][j] = 'O';
            }
        }

    }

    private void bfs(int i, int j, char[][] board, int row, int col) {
        Deque<Point> queue = new LinkedList<>();
        queue.offer(new Point(i, j));
        while (!queue.isEmpty()) {
            Point tmp = queue.poll();
            if (tmp.x >= 0 && tmp.x < row && tmp.y >= 0 && tmp.y < col && board[tmp.x][tmp.y] == 'O') {
                board[tmp.x][tmp.y] = 'B';
                for (int[] dir : dirs) queue.offer(new Point(tmp.x + dir[0], tmp.y + dir[1]));
            }
        }
    }
}
```

### 3.并查集
**思路：** 把边界 O 并且与它连通这些点分在一起
[并查集-维基百科](https://zh.wikipedia.org/wiki/%E5%B9%B6%E6%9F%A5%E9%9B%86)

```
public class Solution {
    int rows, cols;

    public void solve(char[][] board) {
        if(board == null || board.length == 0) return;

        rows = board.length;
        cols = board[0].length;

        //多申请一个空间
        UnionFind uf = new UnionFind(rows * cols + 1);
        //所有边界的 O 节点都和 dummy 节点合并
        int dummyNode = rows * cols;

        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(board[i][j] == 'O') {
                    //当前节点在边界就和 dummy 合并
                    if(i == 0 || i == rows-1 || j == 0 || j == cols-1) {
                        uf.union( dummyNode,node(i,j));
                    }
                    else {
                        //将上下左右的 O 节点和当前节点合并
                        if(board[i-1][j] == 'O')  uf.union(node(i,j), node(i-1,j));
                        if(board[i+1][j] == 'O')  uf.union(node(i,j), node(i+1,j));
                        if(board[i][j-1] == 'O')  uf.union(node(i,j), node(i, j-1));
                        if( board[i][j+1] == 'O')  uf.union(node(i,j), node(i, j+1));
                    }
                }
            }
        }

        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                //判断是否和 dummy 节点是一类
                if(uf.isConnected(node(i,j), dummyNode)) {
                    board[i][j] = 'O';
                }
                else {
                    board[i][j] = 'X';
                }
            }
        }
    }

    int node(int i, int j) {
        return i * cols + j;
    }
}

class UnionFind {
    int [] parents;
    public UnionFind(int totalNodes) {
        parents = new int[totalNodes];
        for(int i = 0; i < totalNodes; i++) {
            parents[i] = i;
        }
    }

    void union(int node1, int node2) {
        int root1 = find(node1);
        int root2 = find(node2);
        if(root1 != root2) {
            parents[root2] = root1;
        }
    }

    int find(int node) {
        while(parents[node] != node) {
            parents[node] = parents[parents[node]];
            node = parents[node];
        }
        return node;
    }

    boolean isConnected(int node1, int node2) {
        return find(node1) == find(node2);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/surrounded-regions/submissions/)
[powcai](https://leetcode-cn.com/problems/surrounded-regions/solution/dfs-bfs-bing-cha-ji-by-powcai/)
[windliang](https://leetcode-cn.com/problems/surrounded-regions/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-6/)***
