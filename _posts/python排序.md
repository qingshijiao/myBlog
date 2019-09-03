---
title: 【python实例37】排序

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
对10个数进行排序。
# 题解
## 1.
### 1) 程序分析
可以利用选择法，即从后9个比较过程中，选择一个最小的与第一个元素交换，下次类推，即用第二个元素与后8个进行比较，并进行交换。
也可以用冒泡排序
也可以用 sort() 方法排序

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

# Bubble Sort
a = []
for i in range(10):
    a.append(int(input('enter a number: ')))
print(a)

for i in range(9):
    for j in range(i + 1, 10):
        if a[i] > a[j]:
            a[i], a[j] = a[j], a[i]
print(a)


```

### 3) 效果
```
enter a number: 9
enter a number: 8
enter a number: 7
enter a number: 5
enter a number: 6
enter a number: 3
enter a number: 2
enter a number: 1
enter a number: 4
enter a number: 10
[9, 8, 7, 5, 6, 3, 2, 1, 4, 10]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
