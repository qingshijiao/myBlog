---
title: 59. 螺旋矩阵 II（Spiral Matrix II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:
```
输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.外围填充
**思路：**
![](https://pic.leetcode-cn.com/ccff416fa39887c938d36fec8e490e1861813d3bba7836eda941426f13420759-Picture1.png)
```
class Solution {
    public int[][] generateMatrix(int n) {
        int l = 0, r = n - 1, t = 0, b = n - 1;
        int[][] mat = new int[n][n];
        int num = 1, tar = n * n;
        while(num <= tar){
            for(int i = l; i <= r; i++) mat[t][i] = num++; // left to right.
            t++;
            for(int i = t; i <= b; i++) mat[i][r] = num++; // top to bottom.
            r--;
            for(int i = r; i >= l; i--) mat[b][i] = num++; // right to left.
            b--;
            for(int i = b; i >= t; i--) mat[i][l] = num++; // bottom to top.
            l++;
        }
        return mat;
    }

}
```

### 2.不同遍历方式
**思路：**
![](https://pic.leetcode-cn.com/5254ec0ff6bec6d954e9abea05d92d8cdcd5136662d2695883bf9d167d8658a9-2019-07-27_124436.jpg)

```
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        for(int s = 0, e = n - 1, m = 1; s<=e ; s++,e--){
            if(s==e) res[s][e] = m++;
            for (int j = s; j <= e-1; j++) res[s][j] = m++;
            for (int i = s; i <= e-1; i++) res[i][e] = m++;
            for (int j = e; j >= s+1; j--) res[e][j] = m++;
            for (int i = e; i >= s+1; i--) res[i][s] = m++;
        }
        return res;

    }

}
```


### 3.python
**思路：**
```
||  =>  |9|  =>  |8|      |6 7|      |4 5|      |1 2 3|
		 |9|  =>  |9 8|  =>  |9 6|  =>  |8 9 4|
				     |8 7|      |7 6 5|


```

```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        r, n = [[n**2]], n**2
        while n > 1: n, r = n - len(r), [[*range(n - len(r), n)]] + [*zip(*r[::-1])]
        return r

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/spiral-matrix-ii/submissions/)
[jyd](https://leetcode-cn.com/problems/spiral-matrix-ii/solution/spiral-matrix-ii-mo-ni-fa-she-ding-bian-jie-qing-x/)
[mei-de-gan-qing-de-fu-du-ya](https://leetcode-cn.com/problems/spiral-matrix-ii/solution/yang-cong-bian-li-tian-chong-fa-by-mei-de-gan-qing/)
[QQqun902025048](https://leetcode-cn.com/problems/spiral-matrix-ii/solution/python-3xing-by-knifezhu/)***
