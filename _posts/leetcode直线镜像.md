---
title: 356.直线镜像(Line Reflection)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given n points on a 2D plane, find if there is such a line parallel to y-axis that reflect the given set of points.

Example 1:
```
Given points = [[1,1],[-1,1]], return true.
```
Example 2:
```
Given points = [[1,1],[-1,-1]], return false.
```

**Follow up:**
- Could you do better than O(n2)?

**Hint:**

- Find the smallest and largest x-value for all points.
- If there is a line then it should be at y = (minX + maxX) / 2.
- For each point, make sure that it has a reflected point in the opposite side.


#### Solution

Language: **Java**

```java
​public class Solution {
    public boolean isReflected(int[][] points) {
        if (points == null || points.length == 0) return true;
        Map<List<Integer>, Integer> map = new HashMap<>();
        for(int[] point: points) {
            List<Integer> key = new ArrayList<>(2);
            key.add(point[0]);
            key.add(point[1]);
            Integer count = map.get(key);
            if (count == null) count = 1; else count ++;
            map.put(key, count);
        }
        int mid = 0;
        for(int[] point: points) mid += point[0];
        // mid /= points.length;

        while (!map.isEmpty()) {
            List<Integer> key1 = map.keySet().iterator().next();
            Integer count1 = map.get(key1);

            if (key1.get(0) * points.length == mid) {
                count1 --;
                if (count1 == 0) map.remove(key1); else map.put(key1, count1);
                continue;
            }

            List<Integer> key2 = new ArrayList<>(2);
            key2.add(2 * mid / points.length - key1.get(0));
            key2.add(key1.get(1));

            if (key1.equals(key2)) {
                if (count1 < 2) return false;
                count1 -= 2;
                if (count1 == 0) map.remove(key1); else map.put(key1, count1);
            } else {
                count1 --;
                if (count1 == 0) map.remove(key1); else map.put(key1, count1);

                Integer count2 = map.get(key2);
                if (count2 == null) return false;
                count2 --;
                if (count2 == 0) map.remove(key2); else map.put(key2, count2);
            }
        }
        return true;
    }
}
```

---
***参考:
[jmspan](https://blog.csdn.net/jmspan/article/details/51688862)***
