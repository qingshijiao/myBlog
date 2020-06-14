---
title: 478. 在圆内随机生成点 (Generate Random Point in a Circle)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [478\. 在圆内随机生成点](https://leetcode-cn.com/problems/generate-random-point-in-a-circle/)

Difficulty: **中等**


给定圆的半径和圆心的 x、y 坐标，写一个在圆中产生均匀随机点的函数 `randPoint` 。

说明:

1.  输入值和输出值都将是。
2.  圆的半径和圆心的 x、y 坐标将作为参数传递给类的构造函数。
3.  圆周上的点也认为是在圆中。
4.  `randPoint` 返回一个包含随机点的x坐标和y坐标的大小为2的数组。

**示例 1：**

```
输入: 
["Solution","randPoint","randPoint","randPoint"]
[[1,0,0],[],[],[]]
输出: [null,[-0.72939,-0.65505],[-0.78502,-0.28626],[-0.83119,-0.19803]]
```

**示例 2：**

```
输入: 
["Solution","randPoint","randPoint","randPoint"]
[[10,5,-7.5],[],[],[]]
输出: [null,[11.52438,-8.33273],[2.46992,-16.21705],[11.13430,-12.42337]]
```

**输入语法说明：**

输入是两个列表：调用成员函数名和调用的参数。`Solution` 的构造函数有三个参数，圆的半径、圆心的 x 坐标、圆心的 y 坐标。`randPoint` 没有参数。输入参数是一个列表，即使参数为空，也会输入一个 [] 空列表。


#### Solution

Language: **Java**

```java
class Solution {

    double r, x, y;
    
    Random rand = new Random();
    
    public Solution(double radius, double x_center, double y_center) {
        r = radius;
        x = x_center;
        y = y_center;
    }
    
    public double[] randPoint() {
        double xx = 2 * r * rand.nextDouble() - r;
        double yy = 2 * r * rand.nextDouble() - r;
        while (xx * xx + yy * yy > r * r) {
            xx = 2 * r * rand.nextDouble() - r;
            yy = 2 * r * rand.nextDouble() - r;
        }
        return new double[]{
            x + xx,
            y + yy
        };
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(radius, x_center, y_center);
 * double[] param_1 = obj.randPoint();
 */
```

```java
​
    double radius;
    double x_center;
    double y_center;


    public  Solution(double radius, double x_center, double y_center) {
        this.radius = radius;
        this.x_center = x_center;
        this.y_center = y_center;
    }

    public double[] randPoint() {
        double r = Math.random() * radius * radius;
        double c = Math.PI * 2 * Math.random();
        r = Math.sqrt(r);
        return new double[]{r * Math.sin(c) + x_center, r * Math.cos(c) + y_center};
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(radius, x_center, y_center);
 * double[] param_1 = obj.randPoint();
 */
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/generate-random-point-in-a-circle/)***
