---
title: 348.判定井字棋胜负

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目描述

请在 n × n 的棋盘上，实现一个判定井字棋（Tic-Tac-Toe）胜负的神器，判断每一次玩家落子后，是否有胜出的玩家。

在这个井字棋游戏中，会有 2 名玩家，他们将轮流在棋盘上放置自己的棋子。

在实现这个判定器的过程中，你可以假设以下这些规则一定成立：

- 每一步棋都是在棋盘内的，并且只能被放置在一个空的格子里；
- 一旦游戏中有一名玩家胜出的话，游戏将不能再继续；
- 一个玩家如果在同一行、同一列或者同一斜对角线上都放置了自己的棋子，那么他便获得胜利。

*示例:*
```
给定棋盘边长 n = 3, 玩家 1 的棋子符号是 "X"，玩家 2 的棋子符号是 "O"。

TicTacToe toe = new TicTacToe(3);

toe.move(0, 0, 1); -> 函数返回 0 (此时，暂时没有玩家赢得这场对决)
|X| | |
| | | |    // 玩家 1 在 (0, 0) 落子。
| | | |

toe.move(0, 2, 2); -> 函数返回 0 (暂时没有玩家赢得本场比赛)
|X| |O|
| | | |    // 玩家 2 在 (0, 2) 落子。
| | | |

toe.move(2, 2, 1); -> 函数返回 0 (暂时没有玩家赢得比赛)
|X| |O|
| | | |    // 玩家 1 在 (2, 2) 落子。
| | |X|

toe.move(1, 1, 2); -> 函数返回 0 (暂没有玩家赢得比赛)
|X| |O|
| |O| |    // 玩家 2 在 (1, 1) 落子。
| | |X|

toe.move(2, 0, 1); -> 函数返回 0 (暂无玩家赢得比赛)
|X| |O|
| |O| |    // 玩家 1 在 (2, 0) 落子。
|X| |X|

toe.move(1, 0, 2); -> 函数返回 0 (没有玩家赢得比赛)
|X| |O|
|O|O| |    // 玩家 2 在 (1, 0) 落子.
|X| |X|

toe.move(2, 1, 1); -> 函数返回 1 (此时，玩家 1 赢得了该场比赛)
|X| |O|
|O|O| |    // 玩家 1 在 (2, 1) 落子。
|X|X|X|
```

*进阶:*
```
您有没有可能将每一步的 move() 操作优化到比 O(n2) 更快吗?
```

#### Solution

Language: **python**

```python
​class TicTacToe(object):
    def __init__(self, n):
        self.size = n
        self.board = [[0 for _ in range(n)] for j in range(n)]

    def move(self, row, col, player):
        self.board[row][col] = player #先把棋子放下去
        if self.check(row, col, player): #再判断有没有胜者
            return player

        return 0


    def check(self, row, col, toe):
        row_valid, col_valid = True, True

        for i in range(self.size):
            if self.board[row][i] != toe: #遍历整行
                row_valid = False
            if self.board[i][col] != toe: #遍历整列
                col_valid = False

        if row != col and row + col != self.size - 1: #如果不需要判断对角线就已经可以返回了
            return row_valid or col_valid

        dia_valid1, dia_valid2 = False, False

        if row == col: #判断\对角线，特点是i == j
            dia_valid1 = True
            for i in range(self.size):
                if self.board[i][i] != toe:
                    dia_valid1 = False

        if row + col == self.size - 1: #判断/对角线，特点是i + j == n - 1
            dia_valid2 = True
            for i in range(self.size):
                if self.board[i][self.size - 1 - i] != toe:
                    dia_valid2 = False

        return row_valid or col_valid or dia_valid1 or dia_valid2

# Your TicTacToe object will be instantiated and called as such:
# obj = TicTacToe(n)
# param_1 = obj.move(row,col,player)
```

---
***参考:
[暴躁老哥在线刷题](https://blog.csdn.net/qq_32424059/article/details/90515918)***
