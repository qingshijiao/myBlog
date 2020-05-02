---
title: 391.完美矩形 (Perfect Rectangle)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [391\. 完美矩形](https://leetcode-cn.com/problems/perfect-rectangle/)

Difficulty: **困难**


我们有 N 个与坐标轴对齐的矩形, 其中 N > 0, 判断它们是否能精确地覆盖一个矩形区域。

每个矩形用左下角的点和右上角的点的坐标来表示。例如， 一个单位正方形可以表示为 [1,1,2,2]。 ( 左下角的点的坐标为 (1, 1) 以及右上角的点的坐标为 (2, 2) )。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_perfect.gif)

**示例 1:**

```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [3,2,4,4],
  [1,3,2,4],
  [2,3,3,4]
]

返回 true。5个矩形一起可以精确地覆盖一个矩形区域。
```

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_separated.gif)

**示例 2:**

```
rectangles = [
  [1,1,2,3],
  [1,3,2,4],
  [3,1,4,2],
  [3,2,4,4]
]

返回 false。两个矩形之间有间隔，无法覆盖成一个矩形。
```

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_hole.gif)

**示例 3:**

```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [1,3,2,4],
  [3,2,4,4]
]

返回 false。图形顶端留有间隔，无法覆盖成一个矩形。
```

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_intersect.gif)

**示例 4:**

```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [1,3,2,4],
  [2,2,4,4]
]

返回 false。因为中间有相交区域，虽然形成了矩形，但不是精确覆盖。
```


#### Solution

Language: **Java**

```java
​class Solution {
    int low1 = Integer.MAX_VALUE;
    int low2 = Integer.MAX_VALUE;
    int high1;
    int high2;
    Map<Integer, Map<Integer, int[]>> data = new HashMap<>(500);
    int lng = 0;

    LinkedList<int[]> baseA = new LinkedList<>();
    LinkedList<int[]> baseB = new LinkedList<>();
    LinkedList<int[]> baseC = new LinkedList<>();

    public boolean isRectangleCover(int[][] rectangles) {
        for (int[] tmp : rectangles) {
            boolean flag = initData(tmp);
            if (!flag) {
                return false;
            }
        }
        baseA.add(new int[]{low1, low2, high1, high2});
        return isPerfect();
    }

    public int[] getOne(int lowX, int lowY) {
        Map<Integer, int[]> tmp = data.get(lowX);
        if (tmp == null) {
            return null;
        } else {
            if (tmp.containsKey(lowY)) {
                int[] res = tmp.get(lowY);
                tmp.remove(lowY);
                lng--;
                return res;
            }
            return null;
        }
    }

    public boolean addOne(int[] tmp) {
        int lowX = tmp[0];
        int lowY = tmp[1];
        if (!data.containsKey(lowX)) {
            Map<Integer, int[]> insert = new HashMap<>();
            insert.put(lowY, tmp);
            data.put(lowX, insert);
            lng++;
            return true;
        }
        Map<Integer, int[]> hasInsert = data.get(lowX);
        if (hasInsert.containsKey(lowY)) {
            return false;
        }
        hasInsert.put(lowY, tmp);
        lng++;
        return true;
    }

    private boolean initData(int[] tmp) {
        if (tmp[0] < low1) {
            low1 = tmp[0];
        }
        if (tmp[1] < low2) {
            low2 = tmp[1];
        }
        if (tmp[2] > high1) {
            high1 = tmp[2];
        }
        if (tmp[3] > high2) {
            high2 = tmp[3];
        }
        return addOne(tmp);
    }

    public boolean isPerfect() {
        while (!baseA.isEmpty() && lng != 0) {
            boolean oneFind = false;
            for (int[] tmp : baseA) {
                int[] ps = getOne(tmp[0], tmp[1]);
                if (ps != null) {
                    oneFind = true;
                    if (ps[2] == tmp[2] && ps[3] == tmp[3]) {
                        continue;
                    }
                    if (ps[3] == tmp[3]) {
                        tmp[0] = ps[2];
                        tmp[1] = ps[1];
                        baseB.add(tmp);
                        continue;
                    }
                    if (ps[2] == tmp[2]) {
                        if (ps[3] > tmp[3]) {
                            //增加
                            tmp[1] = tmp[3];
                            tmp[2] = ps[2];
                            tmp[3] = ps[3];
                            boolean f = addOne(tmp);
                            if (!f) {
                                return false;
                            }
                        } else {
                            //单
                            tmp[0] = ps[0];
                            tmp[1] = ps[3];
                            baseB.add(tmp);
                        }
                        continue;
                    } else {
                        if (ps[3] > tmp[3]) {
                            //增加双
                            int ps2 = ps[2];
                            int ps1 = ps[1];
                            ps[0] = tmp[0];
                            ps[1] = tmp[3];
                            boolean f = addOne(ps);
                            if (!f) {
                                return false;
                            }
                            tmp[0] = ps2;
                            tmp[1] = ps1;
                            baseB.add(tmp);
                        } else {
                            //单
                            int ps0 = ps[0];
                            int ps2 = ps[2];
                            int ps3 = ps[3];
                            int tmp2 = tmp[2];
                            tmp[0] = ps0;
                            tmp[1] = ps3;
                            baseB.add(tmp);
                            ps[0] = ps2;
                            ps[2] = tmp2;
                            baseB.add(ps);
                        }
                        continue;
                    }

                } else {
                    baseB.add(tmp);
                    continue;
                }
            }
            if (!oneFind) {
                return false;
            }
            baseC = baseA;
            baseA = baseB;
            baseB = baseC;
            baseB.clear();
        }
        if (baseA.isEmpty() && lng == 0) {
            return true;
        }
        return false;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/perfect-rectangle/submissions/)***
