---
title: 352.将数据流变为多个不相交区间 (Data Stream as Disjoint Intervals)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [352\. 将数据流变为多个不相交区间](https://leetcode-cn.com/problems/data-stream-as-disjoint-intervals/)

Difficulty: **困难**


给定一个非负整数的数据流输入 a<sub style="display: inline;">1</sub>，a<sub style="display: inline;">2</sub>，…，a<sub style="display: inline;">n，</sub>…，将到目前为止看到的数字总结为不相交的区间列表。

例如，假设数据流中的整数为 1，3，7，2，6，…，每次的总结为：

```
[1, 1]
[1, 1], [3, 3]
[1, 1], [3, 3], [7, 7]
[1, 3], [7, 7]
[1, 3], [6, 7]
```

**进阶：**
如果有很多合并，并且与数据流的大小相比，不相交区间的数量很小，该怎么办?

**提示：**
特别感谢 提供了本问题和其测试用例。


#### Solution

Language: **Java**

```java
​class SummaryRanges {

    TreeMap<Integer, Integer> map = new TreeMap<>();

    /** Initialize your data structure here. */
    public SummaryRanges() {

    }

    public void addNum(int val) {
        Map.Entry<Integer, Integer> ceiling = map.ceilingEntry(val);
        Map.Entry<Integer, Integer> floor = map.floorEntry(val);
        boolean mergedCeiling = false, mergedFloor = false;
        int lower = floor == null ? Integer.MIN_VALUE : floor.getValue();
        int upper = ceiling == null ? Integer.MAX_VALUE : ceiling.getKey();
        if (val == lower +1 && val == upper-1) {
            map.remove(upper);
            map.put(floor.getKey(), ceiling.getValue());
        } else if (val == lower + 1) {
            map.put(floor.getKey(), val);
        } else if (val == upper - 1) {
            map.remove(ceiling.getKey());
            map.put(val, ceiling.getValue());
        } else if (val > lower + 1 && val < upper-1) {
            map.put(val, val);
        }
    }

    public int[][] getIntervals() {
        int[][] result = new int[map.size()][];
        int i = 0;
        for (Map.Entry<Integer,Integer> entry : map.entrySet()) {
            result[i++] = new int[]{entry.getKey(), entry.getValue()};
        }
        return result;
    }
}

/**
 * Your SummaryRanges object will be instantiated and called as such:
 * SummaryRanges obj = new SummaryRanges();
 * obj.addNum(val);
 * int[][] param_2 = obj.getIntervals();
 */
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/data-stream-as-disjoint-intervals/submissions/)***
