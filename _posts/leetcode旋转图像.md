---
title: 48. 旋转图像（Rotate Image）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个 n × n 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

**说明：**

你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

示例 1:
```
给定 matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```
示例 2:
```
给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```


# 题解

## 官方题解
### 1.转置 + 翻转
**思路：**

```
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;

    // transpose matrix
    for (int i = 0; i < n; i++) {
      for (int j = i; j < n; j++) {
        int tmp = matrix[j][i];
        matrix[j][i] = matrix[i][j];
        matrix[i][j] = tmp;
      }
    }
    // reverse each row
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n / 2; j++) {
        int tmp = matrix[i][j];
        matrix[i][j] = matrix[i][n - j - 1];
        matrix[i][n - j - 1] = tmp;
      }
    }
  }
}

```
**复杂度分析**
- 时间复杂度：O(N^2)
- 空间复杂度：O(1) 由于旋转操作是 就地 完成的。

### 2.旋转四个矩形
**思路：**

![04](https://i.loli.net/2019/09/17/KPWStIcND9OinMk.png)
![01](https://i.loli.net/2019/09/17/N9zZfK6CAap5bgl.png)
![03](https://i.loli.net/2019/09/17/JNt8dT1D9inzSgB.png)

```
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < n / 2 + n % 2; i++) {
      for (int j = 0; j < n / 2; j++) {
        int[] tmp = new int[4];
        int row = i;
        int col = j;
        for (int k = 0; k < 4; k++) {
          tmp[k] = matrix[row][col];
          int x = row;
          row = col;
          col = n - 1 - x;
        }
        for (int k = 0; k < 4; k++) {
          matrix[row][col] = tmp[(k + 3) % 4];
          int x = row;
          row = col;
          col = n - 1 - x;
        }
      }
    }
  }
}

```
**复杂度分析**
- 时间复杂度：O(N^2)是两重循环的复杂度。
- 空间复杂度：O(1)  由于我们在一次循环中的操作是 就地 完成的，并且我们只用了长度为 4 的临时列表做辅助。

### 3.在单次循环中旋转 4 个矩形
**思路：**

```
class Solution {
  public void rotate(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < (n + 1) / 2; i ++) {
      for (int j = 0; j < n / 2; j++) {
        int temp = matrix[n - 1 - j][i];
        matrix[n - 1 - j][i] = matrix[n - 1 - i][n - j - 1];
        matrix[n - 1 - i][n - j - 1] = matrix[j][n - 1 -i];
        matrix[j][n - 1 - i] = matrix[i][j];
        matrix[i][j] = temp;
      }
    }
  }
}

```
**复杂度分析**
- 时间复杂度：O(N^2)是两重循环的复杂度。
- 空间复杂度：O(1) 由于旋转操作是 就地 完成的。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/rotate-image/solution/xuan-zhuan-tu-xiang-by-leetcode/)***
