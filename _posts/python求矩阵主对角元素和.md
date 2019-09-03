---
title: 【python实例38】求矩阵主对角元素和

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求一个3*3矩阵主对角线元素之和。
# 题解
## 1.
### 1) 程序分析
利用双重for循环控制输入二维数组，再将a[i][i]累加后输出。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

"""
    1  2  3
    4  5  6
    7  8  9
"""
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
sum = 0
for i in range(0, 3):
    sum += matrix[i][i]
print(sum)

```

### 3) 效果
```
15
```

## 2.
### 1) 程序分析
使用 numpy 包生成 二维矩阵
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import numpy as np

a = np.random.randint(1, 100, 9).reshape(3, 3)
print(a)
(m, n) = np.shape(a)
total = 0
for i in range(m):
    for j in range(n):
        if i == j:
            total += a[i, j]

print(total)
```

### 3) 效果
```
[[75 53 89]
 [71 93 12]
 [ 1  6  1]]
169
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
