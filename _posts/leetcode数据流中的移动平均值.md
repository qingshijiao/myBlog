---
title: 346.数据流中的移动平均值 (Moving Average from Data Stream)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目描述

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

For example,

MovingAverage m = new MovingAverage(3);
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3

#### Solution

Language: **Java**

```java
public class MovingAverage {
    private int[] vals;
    private int from, size;
    private long sum;

    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.vals = new int[size];
    }

    public double next(int val) {
        if (size < vals.length) {
            sum += val;
            vals[size++] = val;
        } else {
            sum -= vals[from];
            vals[from] = val;
            from = (from+1) % vals.length;
        }
        return (double)sum / size;
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```

---
***参考:
[jmspan](https://blog.csdn.net/jmspan/article/details/51289338)***
