---
title: 286.墙与门

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目描述
你被给定一个 m × n 的二维网格，网格中有以下三种可能的初始化值：

-1 表示墙或是障碍物
0 表示一扇门
INF 无限表示一个空的房间。然后，我们用 231 - 1 = 2147483647 代表 INF。你可以认为通往门的距离总是小于 2147483647 的。
你要给每个空房间位上填上该房间到 最近 门的距离，如果无法到达门，则填 INF 即可。

示例：

给定二维网格：
```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```
运行完你的函数后，该网格应该变成：
```
3  -1   0   1
2   2   1  -1
1  -1   2  -1
0  -1   3   4
```

#### Solution1 - BFS

Language: **Java**

```java
public class Solution {
    private void tag(int[][] rooms, int row, int col, int dist) {
        if (row < 0 || row >= rooms.length || col < 0 || col >= rooms[row].length) return;
        if (rooms[row][col] == -1 || rooms[row][col] < dist) return;
        rooms[row][col] = dist;
        tag(rooms, row, col-1, dist+1);
        tag(rooms, row, col+1, dist+1);
        tag(rooms, row-1, col, dist+1);
        tag(rooms, row+1, col, dist+1);
    }
    public void wallsAndGates(int[][] rooms) {
        for(int row = 0; row < rooms.length; row ++) {
            for(int col = 0; col < rooms[row].length; col ++) {
                if (rooms[row][col] == 0) tag(rooms, row, col, 0);
            }
        }
    }
}
```

#### Solution2 - DFS

Language: **Java**

```java
public class Solution {
    public void wallsAndGates(int[][] rooms) {
        Position start = new Position(0,0,0);
        Position tail = start;
        for(int row=0; row<rooms.length; row++) {
            for(int col=0; col<rooms[row].length; col++) {
                if (rooms[row][col]==0) {
                    tail.next = new Position(row, col, 0);
                    tail = tail.next;
                }
            }
        }
        Position current = start.next;
        while (current != null) {
            if (current.row >= 0 && current.row < rooms.length && current.col >= 0 && current.col < rooms[current.row].length && rooms[current.row][current.col] >= current.dist) {
                rooms[current.row][current.col] = current.dist;
                tail.next = new Position(current.row, current.col-1, current.dist+1);
                tail = tail.next;
                tail.next = new Position(current.row, current.col+1, current.dist+1);
                tail = tail.next;
                tail.next = new Position(current.row-1, current.col, current.dist+1);
                tail = tail.next;
                tail.next = new Position(current.row+1, current.col, current.dist+1);
                tail = tail.next;
            }
            current = current.next;
        }
    }
}
class Position {
    int row, col, dist;
    Position next;
    Position(int row, int col, int dist) {
        this.row = row;
        this.col = col;
        this.dist = dist;
    }
}
```

---
***参考：
[jmspan](https://blog.csdn.net/jmspan/article/details/51158397)***
