---
title: 304.二维区域和检索 - 矩阵不可变(Range Sum Query 2D - Immutable)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [304\. 二维区域和检索 - 矩阵不可变](https://leetcode-cn.com/problems/range-sum-query-2d-immutable/)

Difficulty: **中等**


给定一个二维矩阵，计算其子矩形范围内元素的总和，该子矩阵的左上角为 (_row_1, _col_1) ，右下角为 (_row_2, _col_2)。

![Range Sum Query 2D](https://assets.leetcode-cn.com/aliyun-lc-upload/images/304.png)
<small style="display: inline;">上图子矩阵左上角 (row1, col1) = **(2, 1)** ，右下角(row2, col2) = **(4, 3)，**该子矩形内元素的总和为 8。</small>

**示例:**

```
给定 matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```

**说明:**

1.  你可以假设矩阵不可变。
2.  会多次调用 _sumRegion _方法_。_
3.  你可以假设 _row_1 ≤ _row_2 且 _col_1 ≤ _col_2。


#### Solution1 - 暴力法

Language: **Java**
time:O(mn) space:O(1)
```java
​private int[][] data;

public NumMatrix(int[][] matrix) {
    data = matrix;
}

public int sumRegion(int row1, int col1, int row2, int col2) {
    int sum = 0;
    for (int r = row1; r <= row2; r++) {
        for (int c = col1; c <= col2; c++) {
            sum += data[r][c];
        }
    }
    return sum;
}
```

#### Solution2 - 缓存行

Language: **Java**
time:O(m) space:O(mn)
```java
private int[][] dp;

public NumMatrix(int[][] matrix) {
    if (matrix.length == 0 || matrix[0].length == 0) return;
    dp = new int[matrix.length][matrix[0].length + 1];
    for (int r = 0; r < matrix.length; r++) {
        for (int c = 0; c < matrix[0].length; c++) {
            dp[r][c + 1] = dp[r][c] + matrix[r][c];
        }
    }
}

public int sumRegion(int row1, int col1, int row2, int col2) {
    int sum = 0;
    for (int row = row1; row <= row2; row++) {
        sum += dp[row][col2 + 1] - dp[row][col1];
    }
    return sum;
}
```

#### Solution3 - 智能缓存

![](https://pic.leetcode-cn.com/dca167f68285ff2353eb3c186792098aaf866459958af0bf0dbe8c82602e2fa0-image.png)
![](https://pic.leetcode-cn.com/d4ad28b52f13edcc7fa09517e2f425d9b4dfbaaad7b56a9ec0b1e7e97e8e0888-image.png)
![](https://pic.leetcode-cn.com/da44239ca4e857d4d1974f449a3f283a3863403d5ce677f86bd61fb63b34ac04-image.png)
![](https://pic.leetcode-cn.com/227db43a25fb52ddccbc07c09afdc66ea60f97f8d636bbdaf68f167005bf6f75-image.png)
Language: **Java**
time:O(1) space:O(mn)
```java
class NumMatrix {

    int[][] dp;
    public NumMatrix(int[][] matrix) {
        if(   matrix           == null
       || matrix.length    == 0
       || matrix[0].length == 0   ){
        return;
        }
        dp = new int[matrix.length + 1][matrix[0].length + 1];
        for (int i = 1; i < dp.length; i++) {
            for (int j = 1; j < dp[0].length; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j- 1] - dp[i - 1][j - 1] + matrix[i - 1][j - 1];
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return dp[row2 + 1][col2 + 1] - dp[row1][col2 + 1] - dp[row2 + 1][col1] + dp[row1][col1];
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/range-sum-query-2d-immutable/solution/er-wei-qu-yu-he-jian-suo-ju-zhen-bu-ke-bian-by-lee/)***
