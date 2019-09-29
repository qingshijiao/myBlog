---
title: 74. 搜索二维矩阵（Search a 2D Matrix）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。


示例 1:
```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true
```
示例 2:
```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false
```

# 题解

## 官方题解
### 1.二分查找
**思路：**
![](https://pic.leetcode-cn.com/7de6ef012f490979bd93ff358ea0170e060512c923e4a998971e16f58ca3573d-image.png)
```
class Solution {
  public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length;
    if (m == 0) return false;
    int n = matrix[0].length;

    // 二分查找
    int left = 0, right = m * n - 1;
    int pivotIdx, pivotElement;
    while (left <= right) {
      pivotIdx = (left + right) / 2;
      pivotElement = matrix[pivotIdx / n][pivotIdx % n];
      if (target == pivotElement) return true;
      else {
        if (target < pivotElement) right = pivotIdx - 1;
        else left = pivotIdx + 1;
      }
    }
    return false;
  }
}
```
**复杂度分析：**
- 时间复杂度：由于是标准的二分查找，时间复杂度为 O(log(mn))。
- 空间复杂度：O(1)。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/search-a-2d-matrix/solution/sou-suo-er-wei-ju-zhen-by-leetcode/)***
