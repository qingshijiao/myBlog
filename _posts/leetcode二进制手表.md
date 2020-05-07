---
title: 401.二进制手表 (Binary Watch)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [401\. 二进制手表](https://leetcode-cn.com/problems/binary-watch/)

Difficulty: **简单**


二进制手表顶部有 4 个 LED 代表**小时（0-11）**，底部的 6 个 LED 代表**分钟（0-59）**。

每个 LED 代表一个 0 或 1，最低位在右侧。

![](https://upload.wikimedia.org/wikipedia/commons/8/8b/Binary_clock_samui_moon.jpg)

例如，上面的二进制手表读取 “3:25”。

给定一个非负整数 _n _代表当前 LED 亮着的数量，返回所有可能的时间。

**案例:**

```
输入: n = 1
返回: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```

**注意事项:**

*   输出的顺序没有要求。
*   小时不会以零开头，比如 “01:00” 是不允许的，应为 “1:00”。
*   分钟必须由两位数组成，可能会以零开头，比如 “10:2” 是无效的，应为 “10:02”。


#### Solution

Language: **Java**

```java
​class Solution {
    List<String> res = new ArrayList<String>();
    public void backTrack(int[] arr, int depth, int num, int h, int m){
        if(h > 11 || m > 59){
            return;
        }
        if(num == 0){
            StringBuilder hour = new StringBuilder();
            hour.append(h);
            hour.append(":");
            if(m < 10){
                hour.append(0);
            }
            hour.append(m);
            res.add(new String(hour));
            return;
        }
        for(int i = depth; i < arr.length; i++){
            if(i < 4){
                h = h + arr[i];
            }else{
                m = m + arr[i];
            }
            backTrack(arr, i+1, num-1, h, m);
            if(i < 4){
                h = h - arr[i];
            }else{
                m = m - arr[i];
            }
        }
    }
    public List<String> readBinaryWatch(int num) {
        int[] arr = {8,4,2,1,32,16,8,4,2,1};
        if(num < 0 || num > 10){
            return res;
        }
        backTrack(arr, 0, num, 0, 0);
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/binary-watch/submissions/)***
