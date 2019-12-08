---
title: 221.最大正方形（Maximal Square）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [221\. 最大正方形](https://leetcode-cn.com/problems/maximal-square/)

Difficulty: **中等**


在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

**示例:**

```
输入:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```


#### Solution1 - 暴力法

Language: **Java**
time:O((mn)2) space:O(1)
```java
​public class Solution {
    public int maximalSquare(char[][] matrix) {
        int rows = matrix.length, cols = rows > 0 ? matrix[0].length : 0;
        int maxsqlen = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == '1') {
                    int sqlen = 1;
                    boolean flag = true;
                    while (sqlen + i < rows && sqlen + j < cols && flag) {
                        for (int k = j; k <= sqlen + j; k++) {
                            if (matrix[i + sqlen][k] == '0') {
                                flag = false;
                                break;
                            }
                        }
                        for (int k = i; k <= sqlen + i; k++) {
                            if (matrix[k][j + sqlen] == '0') {
                                flag = false;
                                break;
                            }
                        }
                        if (flag)
                            sqlen++;
                    }
                    if (maxsqlen < sqlen) {
                        maxsqlen = sqlen;
                    }
                }
            }
        }
        return maxsqlen * maxsqlen;
    }
}

```

#### Solution2 - 动态规划法

![](https://pic.leetcode-cn.com/28657155fcebc3f210982e889ceef89f6295fb48999222bfe0e52514158c446e-image.png)

Language: **Java**
time:O(mn) space:O(mn)
```java
​public class Solution {
    public int maximalSquare(char[][] matrix) {
        int rows = matrix.length, cols = rows > 0 ? matrix[0].length : 0;
        int[][] dp = new int[rows + 1][cols + 1];
        int maxsqlen = 0;
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                if (matrix[i-1][j-1] == '1'){
                    dp[i][j] = Math.min(Math.min(dp[i][j - 1], dp[i - 1][j]), dp[i - 1][j - 1]) + 1;
                    maxsqlen = Math.max(maxsqlen, dp[i][j]);
                }
            }
        }
        return maxsqlen * maxsqlen;
    }
}

```

#### Solution3 - 动态规划法优化

![](https://pic.leetcode-cn.com/f4ab84cf1059b98caa3ec1eb590853850b64626838f425b921e03856f988bf09-image.png)

Language: **Java**
time:O(mn) space:O(n)
```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        int rows = matrix.length, cols = rows > 0 ? matrix[0].length : 0;
        int[] dp = new int[cols + 1];
        int maxsqlen = 0, prev = 0;
        for (int i = 1; i <= rows; i++) {
            for (int j = 1; j <= cols; j++) {
                int temp = dp[j];
                if (matrix[i - 1][j - 1] == '1') {
                    dp[j] = Math.min(Math.min(dp[j - 1], prev), dp[j]) + 1;
                    maxsqlen = Math.max(maxsqlen, dp[j]);
                } else {
                    dp[j] = 0;
                }
                prev = temp;
            }
        }
        return maxsqlen * maxsqlen;
    }
}

```
#### Solution4 - 行与行之间进行与运算

Language: **Java**
```java
class Solution {
    private char[][] global_matrix;
    private int global_row, global_col;
    private int res = 0;

    public int maximalSquare(char[][] matrix) {
        global_matrix = matrix;
        global_row = matrix.length;
        if (global_row == 0)
            return 0;
        global_col = matrix[0].length;

        for (int i = 0; i < global_row - res; ++i)
            and_operate(i);

        return res * res;
    }

    //每行进行与操作
    private void and_operate(int row) {
        char[] base = global_matrix[row].clone();
        calculate(base, 1);
        char[] next;
        for (int i = row + 1; i < global_row; ++i) {
            next = global_matrix[i];
            for (int j = 0; j < global_col; ++j)
                base[j] &= next[j];//直接与，得到'1'或'0'(都为'1'则为'1')

            if (calculate(base, i - row + 1))
                return;
        }
    }

    //计算1连续出现的次数
    private boolean calculate(char[] array, int limit) {
        int count = 0;
        boolean all_zero = true;
        for (int j = 0; j < global_col; ++j) {
            if (array[j] == '1') {
                all_zero = false;
                ++count;
                if (count == limit) {
                    res = Math.max(res, limit);
                    return false;
                }
            } else
                count = 0;
        }
        return all_zero;
    }
}

```

#### Solution5 - 三者取最小+1

![](https://pic.leetcode-cn.com/8c4bf78cf6396c40291e40c25d34ef56bd524313c2aa863f3a20c1f004f32ab0-image.png)

Language: **Java**
```java
public int maximalSquare(char[][] matrix) {
    // base condition
    if (matrix == null || matrix.length < 1 || matrix[0].length < 1) return 0;

    int height = matrix.length;
    int width = matrix[0].length;
    int maxSide = 0;

    // 相当于已经预处理新增第一行、第一列均为0
//        int[][] dp = new int[height + 1][width + 1];
    int[] dp = new int[width + 1];
    int northwest = 0; // 西北角、左上角

//        for (int row = 0; row < height; row++) {
    for (char[] chars : matrix) {
        for (int col = 0; col < width; col++) {
            int nextNorthwest = dp[col + 1];
            if (chars[col] == '1') {
//                    dp[row + 1][col + 1] = Math.min(Math.min(dp[row + 1][col], dp[row][col + 1]), dp[row][col]) + 1;
                dp[col + 1] = Math.min(Math.min(dp[col], dp[col + 1]), northwest) + 1;

//                    maxSide = Math.max(maxSide, dp[row + 1][col + 1]);
                maxSide = Math.max(maxSide, dp[col + 1]);
            } else {
                dp[col + 1] = 0;
            }
            northwest = nextNorthwest;
        }
    }
    return maxSide * maxSide;
}


```

```java
class Solution {
    /**
     * num[height-1][width-1]对应height*width子矩形"最大正方形"的边长
     */
    static int[][] num;

    /**
     * 矩形内"最大正方形"的边长
     */
    static int area;

    /**
     * 用时最快 https://leetcode-cn.com/submissions/detail/36261372/
     * <p>
     * 思路：对于矩形的任意子矩形，定义：该子矩形内以右下角顶点为顶点的最大正方形为该子矩形的"最大正方形"
     */
    public static int maximalSquare(char[][] matrix) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        // 矩阵的高
        int height = matrix.length;
        // 矩阵的宽
        int width = matrix[0].length;
        num = new int[height][width];
        area = 0;
        for (int i = 0; i < height; i++) {
            for (int j = 0; j < width; j++) {
                num[i][j] = -1;
            }
        }
        squareSearch(matrix, height, width);
        return area * area;
    }

    /**
     * 获得height*width子矩形"最大正方形"的边长（此处"最大正方形"定义见上面"思路"）
     */
    private static int squareSearch(char[][] matrix, int height, int width) {
        if (height < 1 || width < 1) {
            return 0;
        }
        if (num[height - 1][width - 1] != -1) {
            return num[height - 1][width - 1];
        }

        // 左半侧子矩形"最大正方形"的边长
        int left = squareSearch(matrix, height, width - 1);
        // 上半侧子矩形"最大正方形"的边长
        int upper = squareSearch(matrix, height - 1, width);
        // 左上角子矩形"最大正方形"的边长
        int upLeft = squareSearch(matrix, height - 1, width - 1);

        // 上面3个长度的最小值
        int min = Math.min(Math.min(left, upper), upLeft);

        // 右下角顶点为'0'则该子矩形"最大正方形"的边长为0
        if (matrix[height - 1][width - 1] == '0') {
            num[height - 1][width - 1] = 0;
        } else {
            // 该子矩形"最大正方形"的边长
            num[height - 1][width - 1] = min + 1;
            area = Math.max(num[height - 1][width - 1], area);
        }
        return num[height - 1][width - 1];
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/maximal-square/solution/zui-da-zheng-fang-xing-by-leetcode/)
[gfu](https://leetcode-cn.com/problems/maximal-square/solution/xing-yu-xing-zhi-jian-jin-xing-yu-cao-zuo-zai-ji-s/)
[lzhlyle](https://leetcode-cn.com/problems/maximal-square/solution/li-jie-san-zhe-qu-zui-xiao-1-by-lzhlyle/)***
