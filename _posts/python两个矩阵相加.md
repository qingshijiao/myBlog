---
title: 【python实例44】两个矩阵相加

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
两个 3 行 3 列的矩阵，实现其对应位置的数据相加，并返回一个新矩阵：
```
X = [[12,7,3],
    [4 ,5,6],
    [7 ,8,9]]

Y = [[5,8,1],
    [6,7,3],
    [4,5,9]]
```
# 题解
## 1.
### 1) 程序分析
创建一个新的 3 行 3 列的矩阵，使用 for 迭代并取出 X 和 Y 矩阵中对应位置的值，相加后放到新矩阵的对应位置中。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


X = [[12, 7, 3],
     [4, 5, 6],
     [7, 8, 9]]

Y = [[5, 8, 1],
     [6, 7, 3],
     [4, 5, 9]]

result = [[0, 0, 0],
          [0, 0, 0],
          [0, 0, 0]]

# 迭代输出行
for i in range(len(X)):
    # 迭代输出列
    for j in range(len(X[0])):
        result[i][j] = X[i][j] + Y[i][j]

for r in result:
    print(r)

```

### 3) 效果
```
[17, 15, 4]
[10, 12, 9]
[11, 13, 18]
```

## 2.
### 1) 程序分析
创建一个新的 3 行 3 列的矩阵，使用 for 迭代并取出 X 和 Y 矩阵中对应位置的值，相加后放到新矩阵的对应位置中。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import numpy as np

a = np.random.randint(0, 100, 9).reshape(3, 3)
b = np.random.randint(0, 100, 9).reshape(3, 3)

print(a + b)

```

### 3) 效果
```
[[ 89 158 173]
 [ 22  19 122]
 [105  77  94]]
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
