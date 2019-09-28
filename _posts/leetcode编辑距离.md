---
title: 72. 编辑距离（Edit Distance）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符
2. 删除一个字符
3. 替换一个字符


示例 1:
```
输入: word1 = "horse", word2 = "ros"
输出: 3
解释:
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```
示例 2:
```
输入: word1 = "intention", word2 = "execution"
输出: 5
解释:
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.暴力递归
**思路：**
```
class Solution {
    String w1, w2;
    public int minDistance(String word1, String word2) {
        w1 = word1;
        w2 = word2;
        return dp(word1.length() - 1, word2.length() - 1);
    }

    public int dp(int i, int j){
        if (i == -1){
            return j + 1;
        }
        if (j == -1){
            return i + 1;
        }

        if (w1.charAt(i) == w2.charAt(j)) {
            //跳过
            return dp(i - 1, j - 1);
        } else {
            // 插入 删除 替换
            return Math.min(Math.min(dp(i, j - 1) + 1, dp(i - 1, j) + 1), dp(i - 1, j - 1) + 1);
        }
    }
}
```


### 2.记忆法递归
**思路：** 存储递归数据

### 3.动态规划
**思路：** 二维数组
![](https://pic.leetcode-cn.com/501e2518592c5100ca7863f4ebcf0b1c45c72f6b7b5e052087e6cda371cba462-file_1567564774431)

```
class Solution {
    public int minDistance(String word1, String word2) {
        int n1 = word1.length();
        int n2 = word2.length();
        int[][] dp = new int[n1 + 1][n2 + 1];
        // 第一行
        for (int j = 1; j <= n2; j++) dp[0][j] = dp[0][j - 1] + 1;
        // 第一列
        for (int i = 1; i <= n1; i++) dp[i][0] = dp[i - 1][0] + 1;

        for (int i = 1; i <= n1; i++) {
            for (int j = 1; j <= n2; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) dp[i][j] = dp[i - 1][j - 1];
                else dp[i][j] = Math.min(Math.min(dp[i - 1][j - 1], dp[i][j - 1]), dp[i - 1][j]) + 1;
            }
        }
        return dp[n1][n2];
    }
}

```


### 4.动态规划优化
**思路：** 一维数组，我们实际用到的只有其 dp[i - 1][j - 1], dp[i][j - 1], dp[i - 1][j]，其相邻的三个数而已，再定义一个变量 prev 维护多余的一个变量就行。

```
class Solution {
    public int minDistance(String word1, String word2) {
        int n1 = word1.length();
        int[] dp = new int[n1 + 1];
        for (int i = 0; i <= n1; i++) dp[i] = i;
        for (char c2: word2.toCharArray()) {
            int prev = dp[0];
            dp[0] += 1;
            for (int i = 1; i <= n1; i++) {
                int t = dp[i];
                if (word1.charAt(i - 1) == c2) dp[i] = prev;
                else {
                    dp[i] = Math.min(prev, Math.min(dp[i - 1], dp[i])) + 1;
                }
                prev = t;
            }
        }
        return dp[n1];
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/sqrtx/submissions/)
[labuladong](https://leetcode-cn.com/problems/edit-distance/solution/bian-ji-ju-chi-mian-shi-ti-xiang-jie-by-labuladong/)
[powcai](https://leetcode-cn.com/problems/edit-distance/solution/zi-di-xiang-shang-he-zi-ding-xiang-xia-by-powcai-3/)***
