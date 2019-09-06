---
title: 【python实例61】打印杨辉三角

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
打印出杨辉三角形（要求打印出10行如下图）。　　
# 题解
## 1.
### 1) 程序分析
递归
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = 10


def fun(i, j):
    if i == j or j == 1:
        return 1
    else:
        return fun(i - 1, j - 1) + fun(i - 1, j)


for i in range(1, n + 1):
    for j in range(1, i + 1):
        print(fun(i, j), end=' ')
    print()

```

### 3) 效果
```
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1
1 6 15 20 15 6 1
1 7 21 35 35 21 7 1
1 8 28 56 70 56 28 8 1
1 9 36 84 126 126 84 36 9 1
```

## 2.
### 1) 程序分析
非递归，递归会造成大量重复运算
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fun(line):
    a = []
    for n in range(line):
        a.append([])
        for m in range(n + 1):
            if m == 0 or m == n:
                a[n].append(1)
            else:
                a[n].append(a[n-1][m-1] + a[n-1][m])
    return a


for a in fun(10):
    for b in a:
        print(b, end=' ')
    print()

```

### 3) 效果
```
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1
1 6 15 20 15 6 1
1 7 21 35 35 21 7 1
1 8 28 56 70 56 28 8 1
1 9 36 84 126 126 84 36 9 1
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
