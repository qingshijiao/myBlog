---
title: 【python实例39】将一个数插入有序数组

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有一个已经排好序的数组。现输入一个数，要求按原来的规律将它插入数组中。
# 题解
## 1.
### 1) 程序分析
首先判断此数是否大于最后一个数，然后再考虑插入中间的数的情况，插入后此元素之后的数，依次后移一个位置。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

l = [1, 2, 3, 4, 5, 6, 8, 9, 10, 11, 12, 13]
print(l)

n = int(input('enter a number: '))
for i in range(len(l)):
    if l[i] <= n < l[i + 1]:
        l.insert(i + 1, n)
        break
print('插入数字后的列表为：\n', l)

```

### 3) 效果
```
[1, 2, 3, 4, 5, 6, 8, 9, 10, 11, 12, 13]
enter a number: 6
插入数字后的列表为：
 [1, 2, 3, 4, 5, 6, 6, 8, 9, 10, 11, 12, 13]
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
