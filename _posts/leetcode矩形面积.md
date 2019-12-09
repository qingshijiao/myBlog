---
title: 223.矩形面积（Rectangle Area）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [223\. 矩形面积](https://leetcode-cn.com/problems/rectangle-area/)

Difficulty: **中等**


在**二维**平面上计算出两个**由直线构成的**矩形重叠后形成的总面积。

每个矩形由其左下顶点和右上顶点坐标表示，如图所示。

![Rectangle Area](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_area.png)

**示例:**

```
输入: -3, 0, 3, 4, 0, -1, 9, 2
输出: 45
```

**说明:** 假设矩形面积不会超出 **int **的范围。


#### Solution

Language: **Java**

```java
​class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        // x; A, E, C, G
        // y; B, F, D, H
        int areaSum = (C - A) * (D - B) + (G - E) * (H - F);
        if (E - C > 0 || G - A < 0 || F - D > 0 || H - B < 0) return areaSum;
        int[] xs = new int[] {A, C, E, G};
        int[] ys = new int[] {B, D, F, H};
        Arrays.sort(xs);
        Arrays.sort(ys);
        int width = xs[2] - xs[1];
        int high = ys[2] - ys[1];
        return areaSum - (width * high);
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/rectangle-area/submissions/)***
