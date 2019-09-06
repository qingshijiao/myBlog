---
title: 【python实例67】简化选择排序

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入数组，最大的与第一个元素交换，最小的与最后一个元素交换，输出数组。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = [2, 3, 5, 1, 9, 8, 7, 6, 4]

maxIndex = 0
minIndex = 0
for i in range(1, 9):
    if a[i] > a[maxIndex]:
        maxIndex = i
    if a[i] < a[minIndex]:
        minIndex = i
a[0], a[maxIndex] = a[maxIndex], a[0]
a[8], a[minIndex] = a[minIndex], a[8]
print(a)

```

### 3) 效果
```
[9, 3, 5, 4, 2, 8, 7, 6, 1]
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = [1, 2, 3, 7, 9, 8]

# 最小的放到最后
minIndex = min(a)
a.remove(minIndex)
a.append(minIndex)
# 最大的放到最前面
maxIndex = max(a)
a.remove(maxIndex)
a.insert(0, maxIndex)

print(a)

```

### 3) 效果
```
[9, 2, 3, 7, 8, 1]
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
