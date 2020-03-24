---
title: 317.离建筑物最近的距离

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目描述:
你是个房地产开发商，想要选择一片空地 建一栋大楼。你想把这栋大楼够造在一个距离周边设施都比较方便的地方，通过调研，你希望从它出发能在 最短的距离和 内抵达周边全部的建筑物。请你计算出这个最佳的选址到周边全部建筑物的 最短距离和。

注意：
```
你只能通过向上、下、左、右四个方向上移动。

给你一个由 0、1 和 2 组成的二维网格，其中：

0 代表你可以自由通过和选择建造的空地
1 代表你无非通行的建筑物
2 代表你无非通行的障碍物
```
示例：
```
输入: [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

输出: 7

解析:
给定三个建筑物 (0,0)、(0,4) 和 (2,2) 以及一个位于 (0,2) 的障碍物。
由于总距离之和 3+3+1=7 最优，所以位置 (1,2) 是符合要求的最优地点，故返回7。
```
注意：
```
你会保证有至少一栋建筑物，如果无法按照上述规则返回建房地点，则请你返回 -1。
```

#### Solution - 栈

![](https://pic.leetcode-cn.com/dc4e0669d1d7cbf759dc367eb1e7473a38c9d633ff70922bb20578f13f2498f0-image.png)

Language: **python**

```python
class Solution:
    def shortestDistance(self, grid: List[List[int]]) -> int:
        from collections import deque
        row = len(grid)
        col = len(grid[0])
        # 我们用一个三维矩阵，[0, 0]表示i, j位置上有多少建筑物可以到这个位置和每个建筑物到这个位置距离之和
        # 为什么要统计有多少个建筑物到这个位置个数呢? 因为我们要找的位置是所有建筑物都能到的位置,但是有的建筑物由于被障碍物或者其他障碍物阻碍
        distance = [[[0, 0] for i in range(col)] for j in range(row)]
        # print(distance)
        homes = set()
        zero_loc = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    homes.add((i, j))
                    # 设置一个标志
                    distance[i][j][0] = -1
                elif grid[i][j] == 0:
                    zero_loc += 1

        if not zero_loc: return -1
        def bfs(i, j):
            step = 0
            queue = deque([(i, j)])
            visited = set([(i, j)])
            while queue:
                n = len(queue)
                for _ in range(n):
                    i, j = queue.pop()
                    distance[i][j][0] += 1
                    distance[i][j][1] += step
                    for x, y in [[0, -1], [-1, 0], [0, 1], [1, 0]]:
                        tmp_i = i + x
                        tmp_j = j + y
                        if 0 <= tmp_i < row and 0 <= tmp_j < col and grid[tmp_i][tmp_j] == 0 and (
                                tmp_i, tmp_j) not in visited:
                            visited.add((tmp_i, tmp_j))
                            queue.appendleft((tmp_i, tmp_j))
                step += 1

        for i, j in homes:
            bfs(i, j)
        return min([b for dis in distance for a, b in dis if a == len(homes)] or [-1])
```

---
***参考: 
[p](https://zhuanlan.zhihu.com/p/89690268)***
