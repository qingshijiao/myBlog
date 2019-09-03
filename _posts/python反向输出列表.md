---
title: 【python实例32】反向输出列表

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
按相反的顺序输出列表的值。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = ['one', 'two', 'three']
for i in a[::-1]:
    print(i)

```

### 3) 效果
```
three
two
one
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = ['one', 'two', 'three']
a.reverse()
print(a)

```

### 3) 效果
```
['three', 'two', 'one']
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
