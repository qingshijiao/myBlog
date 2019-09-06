---
title: 【python实例64】画图-方形和圆

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
利用ellipse 和 rectangle 画图。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from tkinter import *

canvas = Canvas(width=400, height=600, bg='white')
left = 20
right = 50
top = 50
num = 15

for i in range(num):
    canvas.create_oval(250 - right, 250 - left, 250 + right, 250 + left)
    canvas.create_oval(250 - 20, 250 - top, 250 + 20, 250 + top)
    canvas.create_rectangle(20 - 2 * i, 20 - 2 * i, 10 * (i + 2), 10 * (i + 2))
    right += 5
    left += 5
    top += 10

canvas.pack()
mainloop()

```

### 3) 效果
![](https://i.loli.net/2019/09/06/PLCUnusaBEmyhQf.png)


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
