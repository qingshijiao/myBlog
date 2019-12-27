---
title: 252.会议室（Meeting Rooms）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

Example 1:
```
Input: [[0,30],[5,10],[15,20]]
Output: false
```
Example 2:
```
Input: [[7,10],[2,4]]
Output: true
```
**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.


#### Solution - 链表

Language: **Java**

```java
public class Solution {
    public boolean canAttendMeetings(Interval[] intervals) {
        if (intervals == null || intervals.length == 0) return true;
        Arrays.sort(intervals, (Interval i1, Interval i2) -> i1.start != i2.start ? i1.start - i2.start : i1.end - i2.end);
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i].start < intervals[i - 1].end) return false;
        }
        return true;
    }
}
```
---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5012310.html)***
