---
title: 【python实例13】水仙花数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
打印出所有的"水仙花数"，所谓"水仙花数"是指一个三位数，其各位数字立方和等于该数本身。例如：153是一个"水仙花数"，因为153=1的三次方＋5的三次方＋3的三次方。

# 题解
## 1.
### 1) 程序分析
利用for循环控制100-999个数，每个数分解出个位，十位，百位　　　　

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


for i in range(100, 1000):
    a = int(i / 100)
    b = int(i / 10 % 10)
    c = int(i % 10)
    if i == a ** 3 + b ** 3 + c ** 3:
        print(i)

```

### 3) 效果
```
153
370
371
407
```

## 2.
### 1) 程序分析

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


for i in range(100, 1000):
    a = i // 100
    b = i // 10 % 10
    c = i % 10
    if i == a ** 3 + b ** 3 + c ** 3:
        print(i)

```
**说明：** python 3.x 中 // 表示取整

### 3) 效果
```
153
370
371
407
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
