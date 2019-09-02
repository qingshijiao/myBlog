---
title: 【python实例25】阶乘和

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求1+2!+3!+...+20!的和。
# 题解
## 1.
### 1) 程序分析
此程序只是把累加变成了累乘。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

t = 1
s = 0
for i in range(1, 21):
    t *= i
    s += t

print('1! + 2! + 3! + ... + 20! = %d' % s)

```

### 3) 效果
```
1! + 2! + 3! + ... + 20! = 2561327494111820313
```

## 2.
### 1) 程序分析
可以用递归做，但是递归增加了重复计算，可以利用列表存储，存储起来程序和第一个差不多
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fun(n):
    if n == 1:
        return 1
    else:
        return n * fun(n - 1)


s = 0
for i in range(1, 21):
    s = s + fun(i)

print('1! + 2! + 3! + ... + 20! = %d' % s)

```

### 3) 效果
```
1! + 2! + 3! + ... + 20! = 2561327494111820313
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
