---
title: 【python实例7】复制列表

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
将一个列表的数据复制到另一个列表中。

# 题解
## 1.
### 1) 程序分析
使用列表[:]。

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


a = [1, 2, 3]
b = a[:]


print(b)


```

### 3) 效果
```
[1, 2, 3]
```
## 2.
### 1) 程序分析
使用python3的copy()

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


a = [1, 2, 3]
b = a.copy()


print(b)

```
### 3) 效果
```
[1, 2, 3]
```

## 3.
### 1) 程序分析
将一个列表拓展到另一个列表

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


a = [1, 2, 3]
b = []
b.extend(a)


print(b)


```

### 3) 效果
```
[1, 2, 3]
```




---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
