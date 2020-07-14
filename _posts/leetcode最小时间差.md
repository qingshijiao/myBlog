---
title: 539. 最小时间差（Minimum Time Difference）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [539\. 最小时间差](https://leetcode-cn.com/problems/minimum-time-difference/)

Difficulty: **中等**


给定一个 24 小时制（小时:分钟）的时间列表，找出列表中任意两个时间的最小时间差并以分钟数表示。

**示例 1：**

```
输入: ["23:59","00:00"]
输出: 1
```

**备注:**

1.  列表中时间数在 2~20000 之间。
2.  每个时间取值在 00:00~23:59 之间。


#### Solution

Language: **Java**

```java
​class Solution {
    public int findMinDifference(List<String> timePoints) {
        if(timePoints.size() > 1440){
            return 0;
        }
        int[] times = new int[timePoints.size()];
        for (int i = 0; i < timePoints.size(); i++) {
            String s = timePoints.get(i);
            int t = (s.charAt(0) - '0') * 600 + (s.charAt(1) - '0') * 60 + (s.charAt(3) - '0') * 10 + (s.charAt(4) - '0');
            times[i] = t;
        }
        Arrays.sort(times);
        int res = times[0] + 1440 - times[timePoints.size() - 1];
        for (int i = 1; i < timePoints.size(); i++) {
            res = Math.min(res, times[i] - times[i - 1]);
        }
        return res;
       
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/minimum-time-difference/)***
