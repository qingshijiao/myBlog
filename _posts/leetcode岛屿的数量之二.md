---
title: 305.岛屿的数量之二(Number of Islands II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example:
```
Input: m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]]
Output: [1,1,2,3]
```
Explanation:
```
Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

0 0 0
0 0 0
0 0 0
Operation 1: addLand(0, 0) turns the water at grid[0][0] into a land.

1 0 0
0 0 0   Number of islands = 1
0 0 0
Operation 2: addLand(0, 1) turns the water at grid[0][1] into a land.

1 1 0
0 0 0   Number of islands = 1
0 0 0
Operation 3: addLand(1, 2) turns the water at grid[1][2] into a land.

1 1 0
0 0 1   Number of islands = 2
0 0 0
Operation 4: addLand(2, 1) turns the water at grid[2][1] into a land.

1 1 0
0 0 1   Number of islands = 3
0 1 0
```

*Follow up:*

Can you do it in time complexity O(k log mn), where k is the length of the positions?

#### Solution - Union Find

Language: **Java**
time:O(mn) space:O(1)
```java
​class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> rst = new ArrayList<>();
        if (m <= 0 || n <= 0 || positions == null || positions.length == 0) {
            return rst;
        }

        // use an array to hold root number(Big Brother) of each island
        int[] parent = new int[m * n];
        // use an array to hold the size of each region
        int[] rank = new int[m * n];
        // initialize the unionFind with -1, so we know non negative number is a root number
        // and also mean that the island if true, so we can save the space of isIsland array
        Arrays.fill(parent, -1);
        Arrays.fill(rank, 1);

        int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        // count variable is used to count the island in current matrix.
        int count = 0;
        for(int[] position : positions){
            // for each input cell, its initial root number is itself
            int index = position[0] * n + position[1];
            parent[index] = index;
            count++;

            // check neighbor cells
            for(int[] dir : dirs){
                int nextX = position[0] + dir[0];
                int nextY = position[1] + dir[1];
                // the indices of next point
                int nextP = nextX * n + nextY;
                // if the next point is beyond the bound or it's not an island, ignore it.
                if(nextX < 0 || nextX >= m || nextY < 0 || nextY >= n || parent[nextP] == -1){
                    continue;
                }

                // get the root number(Big Brother) of current island
                int roota = compressedFind(parent, index);
                //get the root number(Big Brother) of the next island
                int rootb = compressedFind(parent, nextP);
                //if roota and rootb are different, then we can union two isolated island together,
                // so the num of island - 1
                if (roota != rootb) {
                    // keep balance
                    if (rank[roota] <= rank[rootb]) {
                        parent[roota] = rootb;
                        rank[rootb] += rank[roota];
                    } else {
                        parent[rootb] = roota;
                        rank[roota] += rank[rootb];
                    }
                    count--;
                }
            }

            rst.add(count);
        }

        return rst;
    }

    private int compressedFind(int[] uf, int index) {
        while (index != uf[index]) {
            uf[index] = uf[uf[index]];
            index = uf[index];
        }
        return index;
    }
}
```

---
***参考：
[cherryljr](https://github.com/cherryljr/LeetCode/blob/master/Number%20of%20Islands%20II.java)***
