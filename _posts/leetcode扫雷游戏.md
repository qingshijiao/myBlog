---
title: 529. 扫雷游戏（Minesweeper）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [529\. 扫雷游戏](https://leetcode-cn.com/problems/minesweeper/)

Difficulty: **中等**


让我们一起来玩扫雷游戏！

给定一个代表游戏板的二维字符矩阵。 **'M'** 代表一个**未挖出的**地雷，**'E'** 代表一个**未挖出的**空方块，**'B' **代表没有相邻（上，下，左，右，和所有4个对角线）地雷的**已挖出的**空白方块，**数字**（'1' 到 '8'）表示有多少地雷与这块**已挖出的**方块相邻，**'X'** 则表示一个**已挖出的**地雷。

现在给出在所有**未挖出的**方块中（'M'或者'E'）的下一个点击位置（行和列索引），根据以下规则，返回相应位置被点击后对应的面板：

1.  如果一个地雷（'M'）被挖出，游戏就结束了- 把它改为 **'X'**。
2.  如果一个**没有相邻地雷**的空方块（'E'）被挖出，修改它为（'B'），并且所有和其相邻的方块都应该被递归地揭露。
3.  如果一个**至少与一个地雷相邻**的空方块（'E'）被挖出，修改它为数字（'1'到'8'），表示相邻地雷的数量。
4.  如果在此次点击中，若无更多方块可被揭露，则返回面板。

**示例 1：**

```
输入: 

[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

输出: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

解释:

```

**示例 2：**

```
输入: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

Click : [1,2]

输出: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'X', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

解释:

```

**注意：**

1.  输入矩阵的宽和高的范围为 [1,50]。
2.  点击的位置只能是未被挖出的方块 ('M' 或者 'E')，这也意味着面板至少包含一个可点击的方块。
3.  输入面板不会是游戏结束的状态（即有地雷已被挖出）。
4.  简单起见，未提及的规则在这个问题中可被忽略。例如，当游戏结束时你不需要挖出所有地雷，考虑所有你可能赢得游戏或标记方块的情况。


#### Solution

Language: **Java**

```java
​class Solution {
    int[] dx = {-1, -1, 0, 1, 1, 1, 0, -1}; // 相邻位置
    int[] dy = {0, 1, 1, 1, 0, -1, -1, -1};

    public char[][] updateBoard(char[][] board, int[] click) {
        dfs(board, click[0], click[1]);
        return board;
    }

    public void dfs(char[][] board, int x, int y) {
        int rows = board.length;
        int cols = board[0].length;
        if (x < 0 || x >= rows || y < 0 || y >= cols) {
            return;
        }

        if (board[x][y] == 'E') { // 如果当前为E，才进行判断是否要递归相邻结点
            board[x][y] = 'B';
            int count = judge(board, x, y);
            if (count == 0) { // 如果为0，则进行递归
                for (int i = 0; i < 8; i++) {
                    dfs(board, x + dx[i], y + dy[i]);
                }
            } else { // 如果不为0，则更新当前结点的值为地雷数量
                board[x][y] = (char) (count + '0');
            }
        } else if (board[x][y] == 'M') { // 注意不要用else，否则会递归修改掉已经是数字的位置
            board[x][y] = 'X';
        }
    }

    // 获取当前借点相邻的地雷数量
    public int judge(char[][] board, int x, int y) {
        int r = board.length;
        int c = board[0].length;
        int count = 0;
        for (int i = 0; i < 8; i++) {
            int newX = x + dx[i];
            int newY = y + dy[i];
            if (newX < 0 || newX >= r || newY < 0 || newY >= c) {
                continue;
            }
            if (board[newX][newY] == 'M') {
                count++;
            }
        }
        return count;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/minesweeper/)***
