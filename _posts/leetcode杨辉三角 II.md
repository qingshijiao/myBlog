---
title: 119.杨辉三角 II（Pascal's Triangle II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:
```
输入: 3
输出: [1,3,3,1]
```

**进阶：**

你可以优化你的算法到 O(k) 空间复杂度吗？


# 题解

## 官方题解
暂无


## 其他题解
### 1.动态规划
**思路：**

```
class Solution {
  public List<Integer> getRow(int rowIndex) {
  int pre = 1;
  List<Integer> cur = new ArrayList<>();
  cur.add(1);
  for (int i = 1; i <= rowIndex; i++) {
      for (int j = 1; j < i; j++) {
          int temp = cur.get(j);
          cur.set(j, pre + cur.get(j));
          pre = temp;
      }
      cur.add(1);
  }
  return cur;
}
```

```
public List<Integer> getRow(int rowIndex) {
    int pre = 1;
    List<Integer> cur = new ArrayList<>();
    cur.add(1);
    for (int i = 1; i <= rowIndex; i++) {
        for (int j = i - 1; j > 0; j--) {
            cur.set(j, cur.get(j - 1) + cur.get(j));
        }
        cur.add(1);//补上每层的最后一个 1
    }
    return cur;
}

```


### 2.公式法
**思路：**

![](https://pic.leetcode-cn.com/195de01eae91e09de14dd13daafbef986c42345f2bdef405153a1742175079f4.jpg)

![](https://i.loli.net/2019/10/18/9m5A7ZnCQtHWzyR.png)

![](https://i.loli.net/2019/10/18/kFqNu5v3Ar7Mo1b.png)

```
class Solution {
  public List<Integer> getRow(int rowIndex) {
      List<Integer> ans = new ArrayList<>();
      int N = rowIndex;
      long pre = 1;
      ans.add(1);
      for (int k = 1; k <= N; k++) {
          long cur = pre * (N - k + 1) / k;
          ans.add((int) cur);
          pre = cur;
      }
      return ans;
  }
}
```

**优化的两种方法是比较常用的，一种就是用pre变量将要被覆盖的变量存起来，另一种就是倒着进行。另外求组合数的时候，要防止int的溢出。**

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/pascals-triangle/solution/yang-hui-san-jiao-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/pascals-triangle-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--28/)***
