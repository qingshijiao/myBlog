---
title: 447. 回旋镖的数量（Number of Boomerangs）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [447\. 回旋镖的数量](https://leetcode-cn.com/problems/number-of-boomerangs/)

Difficulty: **简单**


给定平面上_ n_ 对不同的点，“回旋镖” 是由点表示的元组 `(i, j, k)` ，其中 `i` 和 `j` 之间的距离和 `i` 和 `k` 之间的距离相等（**需要考虑元组的顺序**）。

找到所有回旋镖的数量。你可以假设_ n_ 最大为 **500**，所有点的坐标在闭区间 **[-10000, 10000]** 中。

**示例:**

```
输入:
[[0,0],[1,0],[2,0]]

输出:
2

解释:
两个回旋镖为 [[1,0],[0,0],[2,0]] 和 [[1,0],[2,0],[0,0]]
```


#### Solution

Language: **Java**

```java
​public class Solution {
    public int numberOfBoomerangs(int[][] points) {
        Map<Integer, Integer> map = new HashMap();
        int sum = 0;
        for (int[] p: points) {
            map.clear(); // this is faster than new Map!
            for (int [] q: points) {
                int t, x = p[0] - q[0], y = p[1] - q[1], d2 = x * x + y * y;
                sum += t = map.getOrDefault(d2, 0);
                map.put(d2, ++t);
            }
        }
        return sum <<1;
    } 
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/number-of-boomerangs/submissions/)***
