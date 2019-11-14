---
title: 172.阶乘后的零（Factorial Trailing Zeroes）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数 n，返回 n! 结果尾数中零的数量。

示例 1:
```
输入: 3
输出: 0
解释: 3! = 6, 尾数中没有零。
```
示例 2:
```
输入: 5
输出: 1
解释: 5! = 120, 尾数中有 1 个零.
```
**说明:** 你算法的时间复杂度应为 O(log n) 。


# 题解

## 官方题解
暂无

## 其他题解
### 1.求 5 的个数
**思路：**
```
class Solution {
    public int trailingZeroes(int n) {
        int r = 0;
        while (n >= 5) {
            n /= 5;
            r += n;
        }
        return r;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/factorial-trailing-zeroes/submissions/)
[Ronhou](https://leetcode-cn.com/problems/factorial-trailing-zeroes/solution/q172-factorial-trailing-zeroes-by-ronhou/)***
