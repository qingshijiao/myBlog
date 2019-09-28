---
title: 70. 爬楼梯（Climbing Stairs）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：** 给定 n 是一个正整数。

示例 1：
```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

```
示例 2：
```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

# 题解

## 官方题解
### 1.暴力递归
**思路：**
```
public class Solution {
    public int climbStairs(int n) {
        return climb_Stairs(0, n);
    }
    public int climb_Stairs(int i, int n) {
        if (i > n) {
            return 0;
        }
        if (i == n) {
            return 1;
        }
        return climb_Stairs(i + 1, n) + climb_Stairs(i + 2, n);
    }
}

```
**复杂度分析：**
- 时间复杂度：O(2^n)，树形递归的大小为 2^n。
- 空间复杂度：O(n)，递归树的深度可以达到 n 。

### 2.记忆法递归
**思路：** 暴力递归运算中会出现冗余，采用一个数组记录递归过的数据。
```
class Solution {
    public int climbStairs(int n) {
        int memo[] = new int[n + 1];
        return climb_Stairs(0, n, memo);
    }
    public int climb_Stairs(int i, int n, int memo[]) {
        if (i > n) {
            return 0;
        }
        if (i == n) {
            return 1;
        }
        if (memo[i] > 0) {
            return memo[i];
        }
        memo[i] = climb_Stairs(i + 1, n, memo) + climb_Stairs(i + 2, n, memo);
        return memo[i];
    }

}

```
**复杂度分析：**
- 时间复杂度：O(n)，树形递归的大小可以达到 n。
- 空间复杂度：O(n)，递归树的深度可以达到 n 。


### 3.动态规划
**思路：**
dp[i]=dp[i−1]+dp[i−2]
![](https://pic.leetcode-cn.com/Figures/70_Climbing_StairsSlide7.JPG)


```
class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n)，树形递归的大小可以达到 n。
- 空间复杂度：O(n)，递归树的深度可以达到 n 。


### 4.斐波那契数
**思路：**
从思路三中，就可以看出这个其实是一个斐波那契数列。

```
public class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)，单循环到 n，需要计算第 n 个斐波那契数。
- 空间复杂度：O(1)，使用常量级空间。

### 5.Binets 方法
**思路：**
![](https://i.loli.net/2019/09/28/HSjLTohE431kJlX.png)

```
public class Solution {
   public int climbStairs(int n) {
       int[][] q = {{1, 1}, {1, 0}};
       int[][] res = pow(q, n);
       return res[0][0];
   }
   public int[][] pow(int[][] a, int n) {
       int[][] ret = {{1, 0}, {0, 1}};
       while (n > 0) {
           if ((n & 1) == 1) {
               ret = multiply(ret, a);
           }
           n >>= 1;
           a = multiply(a, a);
       }
       return ret;
   }
   public int[][] multiply(int[][] a, int[][] b) {
       int[][] c = new int[2][2];
       for (int i = 0; i < 2; i++) {
           for (int j = 0; j < 2; j++) {
               c[i][j] = a[i][0] * b[0][j] + a[i][1] * b[1][j];
           }
       }
       return c;
   }
}

```
**复杂度分析：**
- 时间复杂度：O(log(n))，遍历 log(n) 位。
- 空间复杂度：O(1)，使用常量级空间。

### 6.斐波那契公式
**思路：**
![](https://i.loli.net/2019/09/28/y2GiK5okPBlpvxR.png)

```
public class Solution {
    public int climbStairs(int n) {
        double sqrt5=Math.sqrt(5);
        double fibn=Math.pow((1+sqrt5)/2,n+1)-Math.pow((1-sqrt5)/2,n+1);
        return (int)(fibn/sqrt5);
    }
}


```
**复杂度分析：**
- 时间复杂度：O(log(n))，pow 方法将会用去 log(n)log(n) 的时间。
- 空间复杂度：O(1)，使用常量级空间。


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/climbing-stairs/solution/pa-lou-ti-by-leetcode/)***
