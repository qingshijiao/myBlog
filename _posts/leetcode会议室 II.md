---
title: 253.会议室 II（Meeting Rooms II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

Example 1:
```
Input: [[0, 30],[5, 10],[15, 20]]
Output: 2
```
Example 2:
```
Input: [[7,10],[2,4]]
Output: 1
```
**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

#### Solution1 - 优先队列

Language: **Java**

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, Comparator.comparing((int[] itv) -> itv[0]));

    PriorityQueue<Integer> heap = new PriorityQueue<>();
    int count = 0;
    for (int[] itv : intervals) {
        if (heap.isEmpty()) {
            count++;
            heap.offer(itv[1]);
        } else {
            if (itv[0] >= heap.peek()) {
                heap.poll();
            } else {
                count++;
            }

            heap.offer(itv[1]);
        }
    }

    return count;
}
```

#### Solution2 - 排序

Language: **Java**

```java
public int minMeetingRooms(Interval[] intervals) {
        if (intervals == null || intervals.length == 0)
            return 0;
        int[] starter = new int[intervals.length];
        int[] ender = new int[intervals.length];
        for (int i = 0; i < intervals.length; i++) {
            starter[i] = intervals[i].start;
            ender[i] = intervals[i].end;
        }
        Arrays.sort(starter);
        Arrays.sort(ender);
        int endPoint = 0;
        int counter = 0;
        for (int i = 0; i < intervals.length; i++) {
            if (starter[i] < ender[endPoint]) {
                counter++;
            }
            else {
                endPoint++;
            }
        }
        return counter;
    }
```

#### Solution3 - 哈希表

Language: **Java**

```java
public int minMeetingRooms(int[][] intervals) {
    TreeMap<Integer, Integer> map = new TreeMap<>();
    for(int[] interval: intervals) {
        int count = map.getOrDefault(interval[0], 0);
        map.put(interval[0], count+1);
        count = map.getOrDefault(interval[1], 0);
        map.put(interval[1], count-1);
    }
    int maxcount = 0;
    int count = 0;
    for(Map.Entry<Integer, Integer> entry: map.entrySet()) {
        count += entry.getValue();
        maxcount = Math.max(maxcount, count);
    }
    return maxcount;
}
```

---
***参考：
[programcreek](https://www.programcreek.com/2014/05/leetcode-meeting-rooms-ii-java/)
[Richardo92](https://www.jianshu.com/p/ab729e7ddac9)***
