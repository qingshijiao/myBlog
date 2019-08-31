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


list = []
for i in range(3):
    x = int(input('integer:\n'))
    list.append(x)
list.sort()
print(list)

```
**说明：** list 用法

### 3) 效果
```
integer:
3
integer:
2
integer:
1
[1, 2, 3]
```
## 2.
### 1) 程序分析
使用排序函数

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


x = int(input("x:"))
y = int(input("y:"))
z = int(input("z:"))
a = {"x": x, "y": y, "z": z}
print('--------分割线--------')
for i in sorted(a, key=a.get):
    print(i, a[i])

```
**说明：** [sorted 用法](https://www.runoob.com/python/python-func-sorted.html)

### 3) 效果
```
x:3
y:2
z:1
--------分割线--------
z 1
y 2
x 3
```

## 3.
### 1) 程序分析
自写排序算法

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


a = []
for i in range(3):
    a.append(int(input('integer:\n')))
n = len(a)
for i in range(0, n):
    for j in range(i, n):
        if a[i] > a[j]:
            tmp = a[i]
            a[i] = a[j]
            a[j] = tmp

print(a)

```

### 3) 效果
```
integer:
3
integer:
2
integer:
1
[1, 2, 3]
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
