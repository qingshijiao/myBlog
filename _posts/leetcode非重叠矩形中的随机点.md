---
title: 497. 非重叠矩形中的随机点 (Random Point in Non-overlapping Rectangles)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [497\. 非重叠矩形中的随机点](https://leetcode-cn.com/problems/random-point-in-non-overlapping-rectangles/)

Difficulty: **中等**


给定一个非重叠轴对齐矩形的列表 `rects`，写一个函数 `pick` 随机均匀地选取矩形覆盖的空间中的整数点。

提示：

1.  **整数点**是具有整数坐标的点。
2.  矩形周边上的点包含在矩形覆盖的空间中。
3.  第 `i` 个矩形 `rects [i] = [x1，y1，x2，y2]`，其中 `[x1，y1]` 是左下角的整数坐标，`[x2，y2]` 是右上角的整数坐标。
4.  每个矩形的长度和宽度不超过 2000。
5.  `1 <= rects.length <= 100`
6.  `pick` 以整数坐标数组 `[p_x, p_y]` 的形式返回一个点。
7.  `pick` 最多被调用10000次。

**示例 1：**

```
输入: 
["Solution","pick","pick","pick"]
[[[[1,1,5,5]]],[],[],[]]
输出: 
[null,[4,1],[4,1],[3,3]]
```

**示例 2：**

```
输入: 
["Solution","pick","pick","pick","pick","pick"]
[[[[-2,-2,-1,-1],[1,0,3,0]]],[],[],[],[],[]]
输出: 
[null,[-1,-2],[2,0],[-2,-1],[3,0],[-2,-2]]
```

**输入语法的说明：**

输入是两个列表：调用的子例程及其参数。`Solution` 的构造函数有一个参数，即矩形数组 `rects`。`pick` 没有参数。参数总是用列表包装的，即使没有也是如此。


#### Solution

Language: **Java**

```java
​class Solution {

     int[] arr;
    int[][] rects;

    public  Solution(int[][] rects) {
        int[] arr = new int[rects.length];
        for (int i = 0; i < arr.length; i++) {
            int v = (rects[i][2] - rects[i][0] + 1) * (rects[i][3] - rects[i][1] + 1);
            if (i == 0) {
                arr[i] = v;
            } else {
                arr[i] = arr[i - 1] + v;
            }
        }
        this.arr = arr;
        this.rects = rects;
    }

    public int[] pick() {
        int r = (int) (Math.random() * arr[arr.length - 1]) + 1;
        int i = this.search(arr, 0, arr.length - 1, r);
        int x = rects[i][2] - rects[i][0] + 1;
        int temp = arr[i] - r;
        return new int[]{rects[i][0] + temp % x, rects[i][1] + temp / x};

    }

    public int search(int[] arr, int s, int e, int key) {
        while (s < e) {
            int mid = (s + e) >> 1;
            if (arr[mid] == key) {
                return mid;
            } else if (arr[mid] > key) {
                e = mid;
            } else {
                s = mid + 1;
            }
        }
        return s;

    }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(rects);
 * int[] param_1 = obj.pick();
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/random-point-in-non-overlapping-rectangles/)***
