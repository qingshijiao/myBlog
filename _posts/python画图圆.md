---
title: 【python实例56】画图-圆

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
画图，学用circle画圆形。
# 题解
## 1.
### 1) 程序分析


### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from tkinter import *

canvas = Canvas(width=800, height=600, bg='yellow')
canvas.pack(expand=YES, fill=BOTH)
k = 1
j = 1
for i in range(0, 26):
    canvas.create_oval(310 - k, 250 - k, 310 + k, 250 + k, width=1)
    k += j
    j += 0.3

mainloop()

```

### 3) 效果

![](https://i.loli.net/2019/09/05/YG9vy4kPbtAFOma.png)

## 2.
### 1) 程序分析
turtle 库

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import turtle

turtle.title("画圆")
turtle.setup(800, 600, 0, 0)
pen = turtle.Turtle()
pen.color("yellow")
pen.width(5)
pen.shape("turtle")
pen.speed(1)
pen.circle(100)

```

### 3) 效果

![](https://i.loli.net/2019/09/05/dTLXQcilwxefh62.png)


## 3.
### 1) 程序分析
plt

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import numpy as np
import matplotlib.pyplot as plt

x = y = np.arange(-11, 11, 0.1)
x, y = np.meshgrid(x, y)
# 圆心为（0，0），半径为1-10
for i in range(1, 11):
    plt.contour(x, y, x ** 2 + y ** 2, [i ** 2])
    # 如果删除下句，得出的图形为椭圆
    plt.axis('scaled')
plt.show()

```

### 3) 效果
![](https://i.loli.net/2019/09/05/8yqQDgLehE4GOmT.png)



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
