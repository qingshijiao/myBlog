---
title: 【python实例36】求100之内的素数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求100之内的素数。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import math

# Output prime numbers within the specified range
# User input data
lower = int(input('Input interval minimum: '))
upper = int(input('Input interval maximum: '))

for num in range(lower, upper + 1):
    if num > 1:
        for i in range(2, int(math.sqrt(num)) + 1):
            if num % i == 0:
                break
        else:
            print(num)

```
**说明：** for 和 else 搭配，遍历完全执行 else，添加 break

### 3) 效果
```
Input interval minimum: 1
Input interval maximum: 100
2
3
5
7
11
13
17
19
23
29
31
37
41
43
47
53
59
61
67
71
73
79
83
89
97
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
