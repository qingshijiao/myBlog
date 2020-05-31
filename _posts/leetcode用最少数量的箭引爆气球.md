---
title: 452. 用最少数量的箭引爆气球（Minimum Number of Arrows to Burst Balloons）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [452\. 用最少数量的箭引爆气球](https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/)

Difficulty: **中等**


在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以y坐标并不重要，因此只要知道开始和结束的x坐标就足够了。开始坐标总是小于结束坐标。平面内最多存在10<sup>4</sup>个气球。

一支弓箭可以沿着x轴从不同点完全垂直地射出。在坐标x处射出一支箭，若有一个气球的直径的开始和结束坐标为 x<sub style="display: inline;">start，</sub>x<sub style="display: inline;">end，</sub> 且满足  x<sub style="display: inline;">start</sub> ≤ x ≤ x<sub style="display: inline;">end，</sub>则该气球会被引爆<sub style="display: inline;">。</sub>可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。

**Example:**

```
输入:
[[10,16], [2,8], [1,6], [7,12]]

输出:
2

解释:
对于该样例，我们可以在x = 6（射爆[2,8],[1,6]两个气球）和 x = 11（射爆另外两个气球）。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int findMinArrowShots(int[][] points) {
        if (points.length == 0) return 0;
        Arrays.sort(points, new Comparator<int[]>(){
            @Override
            public int compare(int[] a, int[] b) {
                return a[1] - b[1];
            }
        });
        
        int count = 1;
        int x_end = points[0][1];
        for (int[] point : points) {
            if (point[0] > x_end) {
                count++;
                x_end = point[1];
            }
        }
        
        return count;
    }
}
```


---
***参考：
[leetcode](https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/submissions/)***
