---
title: 52. N 皇后 II（N-Queens II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/8-queens.png)
上图为 8 皇后问题的一种解法。

给定一个整数 n，返回 n 皇后不同的解决方案的数量。

示例:
```
输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```



# 题解

## 官方题解
### 1.约束编程 + 回溯算法
**思路：**
![](https://pic.leetcode-cn.com/e67ed217a00038ed292ae8cb89c1a8492c7a49e33ec17f633f41c4ece77d6c2c-51_pic.png)
```
class Solution {
  public boolean is_not_under_attack(int row, int col, int n,
                                     int [] rows,
                                     int [] hills,
                                     int [] dales) {
    int res = rows[col] + hills[row - col + 2 * n] + dales[row + col];
    return (res == 0) ? true : false;
  }

  public int backtrack(int row, int count, int n,
                       int [] rows,
                       int [] hills,
                       int [] dales) {
    for (int col = 0; col < n; col++) {
      if (is_not_under_attack(row, col, n, rows, hills, dales)) {
        // place_queen
        rows[col] = 1;
        hills[row - col + 2 * n] = 1;  // "hill" diagonals
        dales[row + col] = 1;   //"dale" diagonals

        // if n queens are already placed
        if (row + 1 == n) count++;
        // if not proceed to place the rest
        else count = backtrack(row + 1, count, n,
                rows, hills, dales);

        // remove queen
        rows[col] = 0;
        hills[row - col + 2 * n] = 0;
        dales[row + col] = 0;
      }
    }
    return count;
  }

  public int totalNQueens(int n) {
    int rows[] = new int[n];
    // "hill" diagonals
    int hills[] = new int[4 * n - 1];
    // "dale" diagonals
    int dales[] = new int[2 * n - 1];

    return backtrack(0, 0, n, rows, hills, dales);
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N!). 放置第 1 个皇后有 N 种可能的方法，放置两个皇后的方法不超过 N (N - 2) ，放置 3 个皇后的方法不超过 N(N - 2)(N - 4) ，以此类推。总体上，时间复杂度为 O(N!) .
- 空间复杂度：需要保存对角线和行的信息。


## 其他题解
### 1.位运算
**思路：**
```
class Solution {
    int res;
    public int totalNQueens(int n) {
        func(0, 0, 0, (1 << n) - 1, n);
        return res;
    }

    public void func(int shu, int pie, int na, int cons, int n){
        if(n == 0){
            res++;
            return;
        }
        int bit = ~(shu | pie | na) & cons;
        while(bit != 0){
            int temp = bit & -bit;
            func(shu | temp, (pie | temp) << 1, (na | temp) >> 1, cons, n - 1);
            bit ^= temp;
        }
    }
}
```

### 2.直接把结果存入数组
**思路：**
```
class Solution {

public int totalNQueens(int n) {
                int[] rs = new int[]{0,1,0,0,2,10,4,40,92,352,724,2680};
        return rs[n];
    }

}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/n-queens-ii/solution/nhuang-hou-ii-by-leetcode/)***
