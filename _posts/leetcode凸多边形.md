---
title: 469.凸多边形 (Convex Polygon)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

Given a list of points that form a polygon when joined sequentially, find if this polygon is convex (Convex polygon definition).

Note:

There are at least 3 and at most 10,000 points.
Coordinates are in the range -10,000 to 10,000.
You may assume the polygon formed by given points is always a simple polygon (Simple polygon definition). In other words, we ensure that exactly two edges intersect at each vertex, and that edges otherwise don't intersect each other.
Example 1:

[[0,0],[0,1],[1,1],[1,0]]

Answer: True

Explanation:

![](https://leetcode.com/static/images/problemset/polygon_convex.png)

Example 2:

[[0,0],[0,10],[10,10],[10,0],[5,5]]

Answer: False

Explanation:

![](https://leetcode.com/static/images/problemset/polygon_not_convex.png)

#### Solution

Language: **c++**

```c++
class Solution {
public:
    bool isConvex(vector<vector<int>>& points) {
        long long n = points.size(), pre = 0, cur = 0;
        for (int i = 0; i < n; ++i) {
            int dx1 = points[(i + 1) % n][0] - points[i][0];
            int dx2 = points[(i + 2) % n][0] - points[i][0];
            int dy1 = points[(i + 1) % n][1] - points[i][1];
            int dy2 = points[(i + 2) % n][1] - points[i][1];
            cur = dx1 * dy2 - dx2 * dy1;
            if (cur != 0) {
                if (cur * pre < 0) return false;
                else pre = cur;
            }
        }
        return true;
    }
};
```
---
***参考:
[grandyang](https://www.cnblogs.com/grandyang/p/6146986.html)***
