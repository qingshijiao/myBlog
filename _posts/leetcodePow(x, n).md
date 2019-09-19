---
title: 50. Pow(x, n)（Pow(x, n)）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例 1:
```
输入: 2.00000, 10
输出: 1024.00000
```
示例 2:
```
输入: 2.10000, 3
输出: 9.26100
```
示例 3:
```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```
**说明:**
> -100.0 < x < 100.0
> n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

# 题解

## 官方题解
### 1.暴力法
**思路：** 不断累乘

```
class Solution {
   public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        double ans = 1;
        for (long i = 0; i < N; i++)
            ans = ans * x;
        return ans;
    }

}

```
**复杂度分析：**
- 时间复杂度：O(n)，我们需要将 x 连乘 n 次。
- 空间复杂度：O(n)，我们只需要一个变量来保存最终 x 的连乘结果。

### 2.快速幂算法（递归）
**思路：**
![](https://i.loli.net/2019/09/19/9O8gQ6NHTRjLVZ3.png)


```
class Solution {
   private double fastPow(double x, long n) {
        if (n == 0) {
            return 1.0;
        }
        double half = fastPow(x, n / 2);
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
    public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        return fastPow(x, N);
    }
}


```
![](https://i.loli.net/2019/09/19/CMqZ7bmQorPsuXS.png)


### 3.
**思路：**
![](https://i.loli.net/2019/09/19/XP3ZkU9f8aKwVnE.png)
![](https://i.loli.net/2019/09/19/Qe2DK1NAsr5P6ly.png)


```
class Solution {
   public double myPow(double x, int n) {
        long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        double ans = 1;
        double current_product = x;
        for (long i = N; i > 0; i /= 2) {
            if ((i % 2) == 1) {
                ans = ans * current_product;
            }
            current_product = current_product * current_product;
        }
        return ans;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(logn). 对每一个 n 的二进制位表示，我们都至多需要累乘 1 次，所以总的时间复杂度为 O(logn) 。
- 空间复杂度：O(1). 我们只需要用到 2 个变量来保存当前的乘积和最终的结果 x 。



## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/powx-n/solution/powx-n-by-leetcode/)***
