---
title: 【python实例19】寻找完数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
一个数如果恰好等于它的因子之和，这个数就称为"完数"。例如6=1＋2＋3.编程找出1000以内的所有完数。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

for i in range(2, 1001):
    sum = 0
    k = []
    for j in range(1, i):
        if i % j == 0:
            sum += j
            k.append(j)
    if sum == i:
        print(i, k)

```

### 3) 效果
```
6 [1, 2, 3]
28 [1, 2, 4, 7, 14]
496 [1, 2, 4, 8, 16, 31, 62, 124, 248]
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
