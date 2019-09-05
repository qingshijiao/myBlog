---
title: 【python实例58】画图-方形

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
画图，学用rectangle画方形。
# 题解
## 1.
### 1) 程序分析
```rectangle(int left, int top, int right, int bottom)```
**参数说明：** (left ，top )为矩形的左上坐标，(right,bottom)为矩形的右下坐标，两者可确定一个矩形的大小
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from tkinter import *

root = Tk()
root.title('Canvas')
canvas = Canvas(root, width=400, height=400, bg='yellow')
x0 = 263
y0 = 263
y1 = 275
x1 = 275
for i in range(19):
    canvas.create_rectangle(x0, y0, x1, y1)
    x0 -= 5
    y0 -= 5
    x1 += 5
    y1 += 5

canvas.pack()
root.mainloop()

```

### 3) 效果
![](https://i.loli.net/2019/09/05/KOtrgmcE4Fukbnv.png)


## 2.
### 1) 程序分析
turtle 库

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import turtle


def drawline(n):
    t = turtle.Pen()
    t.color(0.3, 0.8, 0.6)  # 设置颜色，在0--1之间
    t.begin_fill()  # 开始填充颜色
    for i in range(n):  # 任意边形
        t.forward(50)
        t.left(360 / n)
    t.end_fill()  # 结束填充颜色


drawline(4)
```

### 3) 效果
![](https://i.loli.net/2019/09/05/67ngsip8VWvNhB3.png)



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
