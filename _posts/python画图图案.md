---
title: 【python实例65】画图-图案

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
一个最优美的图案。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import math
from tkinter import *


class PTS:
    def __init__(self):
        self.x = 0
        self.y = 0


points = []


def demo():
    screenx = 400
    screeny = 400
    canvas = Canvas(width=screenx, height=screeny, bg='white')

    AspectRatio = 0.85
    MAXPTS = 15
    h = screeny
    w = screenx
    xcenter = w / 2
    ycenter = h / 2
    radius = (h - 30) / (AspectRatio * 2) - 20
    step = 360 / MAXPTS
    angle = 0.0
    for i in range(MAXPTS):
        rads = angle * math.pi / 180.0
        p = PTS()
        p.x = xcenter + int(math.cos(rads) * radius)
        p.y = ycenter - int(math.sin(rads) * radius * AspectRatio)
        angle += step
        points.append(p)
    canvas.create_oval(xcenter - radius, ycenter - radius,
                       xcenter + radius, ycenter + radius)
    for i in range(MAXPTS):
        for j in range(i, MAXPTS):
            canvas.create_line(points[i].x, points[i].y, points[j].x, points[j].y)

    canvas.pack()
    mainloop()


if __name__ == '__main__':
    demo()

```

### 3) 效果
![](https://i.loli.net/2019/09/06/3UF7iuaWmt8QYSK.png)


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
