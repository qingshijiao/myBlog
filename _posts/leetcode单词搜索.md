---
title: 79. 单词搜索（Word Search）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

示例:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.回溯
**思路：** 深度优先搜索
```
class Solution {
    public boolean exist(char[][] board, String word) {
        if (board.length == 0 || board[0].length == 0){
            return false;
        }
        boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i = 0; i < visited.length; i++) {
            for (int j = 0; j < visited[0].length; j++) {
                visited[i][j] = false;
            }
        }
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (search(board, word, 0, i, j, visited)){
                    return true;
                }
            }
        }
        return false;
    }

    public static boolean search(char[][] board, String word, int index, int i, int j, boolean[][] visited){
        if (index == word.length()){
            return true;
        }
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || visited[i][j] || board[i][j] != word.charAt(index)){
            return false;
        }
        visited[i][j] = true;
        boolean result = search(board, word, index + 1, i - 1, j, visited)
                || search(board, word, index + 1, i + 1, j, visited)
                || search(board, word, index + 1, i, j - 1, visited)
                || search(board, word, index + 1, i, j + 1, visited);
        visited[i][j] = false;
        return result;

    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/word-search/)***
