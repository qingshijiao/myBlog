---
title: 499. 迷宫之三 (The Maze III)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
## 题目
There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up (u), down (d), left (l) or right (r), but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction. There is also a hole in this maze. The ball will drop into the hole if it rolls on to the hole.

Given the ball position, the hole position and the maze, find out how the ball could drop into the hole by moving the shortest distance. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the hole (included). Output the moving directions by using 'u', 'd', 'l' and 'r'. Since there could be several different shortest ways, you should output the lexicographically smallest way. If the ball cannot reach the hole, output "impossible".

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The ball and the hole coordinates are represented by row and column indexes.

Example 1

Input 1: a maze represented by a 2D array

0 0 0 0 0
1 1 0 0 1
0 0 0 0 0
0 1 0 0 1
0 1 0 0 0

Input 2: ball coordinate (rowBall, colBall) = (4, 3)
Input 3: hole coordinate (rowHole, colHole) = (0, 1)

Output: "lul"
Explanation: There are two shortest ways for the ball to drop into the hole.
The first way is left -> up -> left, represented by "lul".
The second way is up -> left, represented by 'ul'.
Both ways have shortest distance 6, but the first way is lexicographically smaller because 'l' < 'u'. So the output is "lul".


![](https://leetcode.com/static/images/problemset/maze_2_example_1.png)

Example 2

Input 1: a maze represented by a 2D array

0 0 0 0 0
1 1 0 0 1
0 0 0 0 0
0 1 0 0 1
0 1 0 0 0

Input 2: ball coordinate (rowBall, colBall) = (4, 3)
Input 3: hole coordinate (rowHole, colHole) = (3, 0)
Output: "impossible"
Explanation: The ball cannot reach the hole.

![](https://leetcode.com/static/images/problemset/maze_2_example_2.png)
 

Note:

There is only one ball and one hole in the maze.
Both the ball and hole exist on an empty space, and they will not be at the same position initially.
The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
The maze contains at least 2 empty spaces, and the width and the height of the maze won't exceed 30.


#### Solution

Language: **c++**
```c++
class Solution {
public:
    vector<vector<int>> dirs{{0,-1},{-1,0},{0,1},{1,0}};
    vector<char> way{'l','u','r','d'};
    string findShortestWay(vector<vector<int>>& maze, vector<int>& ball, vector<int>& hole) {
        int m = maze.size(), n = maze[0].size();
        vector<vector<int>> dists(m, vector<int>(n, INT_MAX));
        unordered_map<int, string> u;
        dists[ball[0]][ball[1]] = 0;
        helper(maze, ball[0], ball[1], hole, dists, u);
        string res = u[hole[0] * n + hole[1]];
        return res.empty() ? "impossible" : res;
    }
    void helper(vector<vector<int>>& maze, int i, int j, vector<int>& hole, vector<vector<int>>& dists, unordered_map<int, string>& u) {
        if (i == hole[0] && j == hole[1]) return;
        int m = maze.size(), n = maze[0].size();
        for (int k = 0; k < 4; ++k) {
            int x = i, y = j, dist = dists[x][y];
            string path = u[x * n + y];
            while (x >= 0 && x < m && y >= 0 && y < n && maze[x][y] == 0 && (x != hole[0] || y != hole[1])) {
                x += dirs[k][0]; y += dirs[k][1]; ++dist;
            }
            if (x != hole[0] || y != hole[1]) {
                x -= dirs[k][0]; y -= dirs[k][1]; --dist;
            }
            path.push_back(way[k]);
            if (dists[x][y] > dist) {
                dists[x][y] = dist;
                u[x * n + y] = path;
                helper(maze, x, y, hole, dists, u);
            } else if (dists[x][y] == dist && u[x * n + y].compare(path) > 0) {
                u[x * n + y] = path;
                helper(maze, x, y, hole, dists, u);
            }
        }
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6746528.html)***
