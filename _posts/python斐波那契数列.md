---
title: 【python实例6】斐波那契数列

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
斐波那契数列。

# 题解
## 1.
### 1) 程序分析
斐波那契数列（Fibonacci sequence），又称黄金分割数列，指的是这样一个数列：0、1、1、2、3、5、8、13、21、34、……。

在数学上，费波那契数列是以递归的方法来定义：

> F0 = 0     (n=0)
> F1 = 1    (n=1)
> Fn = F[n-1]+ F[n-2](n=>2)

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fib(n):
    a, b = 1, 1
    for i in range(n - 1):
        a, b = b, a + b
    return a


print(fib(10))

```
**说明：** list 用法

### 3) 效果
```
55
```
## 2.
### 1) 程序分析
使用递归

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fib(n):
    if (n == 1) or (n == 2):
        return 1
    return fib(n - 1) + fib(n - 2)


print(fib(10))

```
### 3) 效果
```
55
```

## 3.
### 1) 程序分析
存储所有斐波那契数

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fib(n):
    if n == 1:
        return [1]
    if n == 2:
         return [1, 1]
    fibs = [1, 1]
    for i in range(2, n):
        fibs.append(fibs[-1] + fibs[-2])
    return fibs


print(fib(10))

```

### 3) 效果
```
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```



## 4.
### 1) 程序分析
使用[斐波那契数列通项公式](https://zhuanlan.zhihu.com/p/26679684)

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fib(n):
    return 1 / (5 ** 0.5) * ((((1 + (5 ** 0.5)) / 2) ** n) - (((1 - (5 ** 0.5)) / 2) ** n))


print(fib(10))
print(int(fib(10)))

```

### 3) 效果
```
55.000000000000014
55
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
