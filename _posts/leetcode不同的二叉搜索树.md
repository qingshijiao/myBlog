---
title: 96.不同的二叉搜索树（Unique Binary Search Trees）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:
```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```


# 题解

## 官方题解
### 1.动态规划
**思路：**

```
public class Solution {
  public int numTrees(int n) {
    int[] G = new int[n + 1];
    G[0] = 1;
    G[1] = 1;

    for (int i = 2; i <= n; ++i) {
      for (int j = 1; j <= i; ++j) {
        G[i] += G[j - 1] * G[i - j];
      }
    }
    return G[n];
  }
}


```
![](https://i.loli.net/2019/10/07/BZS93gv4LxHwnNm.png)


### 2.数学演绎
**思路：**
![](https://i.loli.net/2019/10/07/AjqcCMNynXVpLIt.png)

```
class Solution {
  public int numTrees(int n) {
    // Note: we should use long here instead of int, otherwise overflow
    long C = 1;
    for (int i = 0; i < n; ++i) {
      C = C * 2 * (2 * i + 1) / (i + 2);
    }
    return (int) C;
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N)，只有一层循环。
- 空间复杂度：O(1)，只需要一个变量来存储中间与最终结果。



## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/unique-binary-search-trees/solution/bu-tong-de-er-cha-sou-suo-shu-by-leetcode/)***
