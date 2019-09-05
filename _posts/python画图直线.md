---
title: 【python实例57】画图-直线

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
画图，学用line画直线。
# 题解

## 1.
### 1) 程序分析
turtle 库

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from tkinter import *

canvas = Canvas(width=300, height=300, bg='green')
canvas.pack(expand=YES, fill=BOTH)
x0 = 263
y0 = 263
y1 = 275
x1 = 275
for i in range(19):
    canvas.create_line(x0, y0, x0, y1, width=1, fill='red')
    x0 = x0 - 5
    y0 = y0 - 5
    x1 = x1 + 5
    y1 = y1 + 5

x0 = 263
y1 = 275
y0 = 263
for i in range(21):
    canvas.create_line(x0, y0, x0, y1, fill='red')
    x0 += 5
    y0 += 5
    y1 += 5

mainloop()

```

### 3) 效果
![](https://i.loli.net/2019/09/05/65PHAvuSf3ajCkU.png)



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


drawline(5)

```

### 3) 效果
![](https://puui.qpic.cn/fans_admin/0/3_500685383_1567662678208/0)



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
