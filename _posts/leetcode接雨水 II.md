---
title: 407. 接雨水 II（Trapping Rain Water II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [407\. 接雨水 II](https://leetcode-cn.com/problems/trapping-rain-water-ii/)

Difficulty: **困难**


给你一个 `m x n` 的矩阵，其中的值均为非负整数，代表二维高度图每个单元的高度，请计算图中形状最多能接多少体积的雨水。

**示例：**

```
给出如下 3x6 的高度图:
[
  [1,4,3,1,3,2],
  [3,2,1,3,2,4],
  [2,3,3,2,3,1]
]

返回 4 。
```

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/rainwater_empty.png)

如上图所示，这是下雨前的高度图`[[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]` 的状态。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/rainwater_fill.png)

下雨后，雨水将会被存储在这些方块中。总的接雨水量是4。

**提示：**

*   `1 <= m, n <= 110`
*   `0 <= heightMap[i][j] <= 20000`


#### Solution

Language: **Java**

```java
​class Solution {

    static int[][] hMap;

    int iM;
    int jM;

    int[][] mapping;

    ArrayList<Point>[] limits;

    public int trapRainWater(int[][] heightMap) {

        hMap = heightMap;

        iM = hMap.length;
        jM = hMap[0].length;

        mapping = new int[iM][];
        limits = new ArrayList[20000];

        int max = 0;

        for (int i = 0; i < iM; i++) {
            int[] row = new int[jM];
            for (int j = 0; j < jM; j++) {
                max = Math.max(max, hMap[i][j]);

                if (i == 0 || i == iM - 1 || j == 0 || j == jM - 1) {
                    Point p = new Point(i, j);

                    ArrayList<Point> limit = limits[hMap[i][j] - 1];

                    if (limit == null) {
                        limit = new ArrayList<>();
                        limits[hMap[i][j] - 1] = limit;
                    }

                    limit.add(p);

                    row[j] = 0;
                } else {
                    row[j] = 1;
                }
            }

            mapping[i] = row;

            // System.out.println(Arrays.toString(row));
        }

        int yield = 0;

        for (int i = 0; i < max; i++) {
            ArrayList<Point> limit = limits[i];

            if (limit == null) {
                continue;
            }
            
            //System.out.println(limit);

            for (int lp = 0; lp < limit.size(); lp++) {
                Point p = limit.get(lp);
                yield += stream(p.x - 1, p.y, hMap[p.x][p.y]);
                yield += stream(p.x + 1, p.y, hMap[p.x][p.y]);
                yield += stream(p.x, p.y - 1, hMap[p.x][p.y]);
                yield += stream(p.x, p.y + 1, hMap[p.x][p.y]);
            }
        }
        
        //System.out.println();
        
        // for (ArrayList<Point> limit : limits) {
        //     if (limit == null) {
        //         continue;
        //     }
        //     System.out.println(limit);
        // }

        return yield;

    }

    int stream(int i, int j, int h) {
        if (i < 0 || i >= iM || j < 0 || j >= jM) {
            return 0;
        }
        if (mapping[i][j] == 0) {
            return 0;
        }
        mapping[i][j] = 0;

        if (h <= hMap[i][j]) {
            Point p = new Point(i, j);

            ArrayList<Point> limit = limits[hMap[i][j] - 1];

            if (limit == null) {
                limit = new ArrayList<>();
                limits[hMap[i][j] - 1] = limit;
            }

            limit.add(p);

            return 0;
        }

        int water = h - hMap[i][j];

        water += stream(i - 1, j, h);
        water += stream(i + 1, j, h);
        water += stream(i, j - 1, h);
        water += stream(i, j + 1, h);

        return water;
    }
}

class Point {
    int x;
    int y;
    int val = 0;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public String toString() {
        return "Point{" +
                "x=" + x +
                ", y=" + y +
                ", val=" + Solution.hMap[x][y] +
                '}';
    }
}
```
---
***参考：
[LeetCode](https://leetcode-cn.com/problems/trapping-rain-water-ii/submissions/)***
