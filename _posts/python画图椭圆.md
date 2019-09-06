---
title: 【python实例63】画图-椭圆

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
画椭圆。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from tkinter import *

x = 360
y = 160
top = y - 30
bottom = y - 30

canvas = Canvas(width=400, height=600, bg='white')
for i in range(20):
    canvas.create_oval(250 - top, 250 - bottom, 250 + top, 250 + bottom)
    top -= 5
    bottom += 5
canvas.pack()
mainloop()

```

### 3) 效果
![](https://i.loli.net/2019/09/06/pFQJTemL61NEhuo.png)


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
