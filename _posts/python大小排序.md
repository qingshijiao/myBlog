---
title: 【python实例5】大小排序

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入三个整数x,y,z，请把这三个数由小到大输出。

# 题解
## 1.
### 1) 程序分析
我们想办法把最小的数放到x上，先将x与y进行比较，如果x>y则将x与y的值进行交换，然后再用x与z进行比较，如果x>z则将x与z的值进行交换，这样能使x最小。：

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
