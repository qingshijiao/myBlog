---
title: 【python实例88】打印星号

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
读取7个数（1—50）的整数值，每读取一个值，程序打印出该值个数的＊。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


for i in range(3):
    n = int(input('input a number:\n'))
    if 1 < n < 50:
        for j in range(n):
            print('*', end='')
    print()

```

### 3) 效果
```
input a number:
9
*********
input a number:
5
*****
input a number:
6
******

```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
