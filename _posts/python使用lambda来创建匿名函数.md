---
title: 【python实例49】使用lambda来创建匿名函数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
使用lambda来创建匿名函数。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


MAXIMUM = lambda x, y: (x > y) * x + (x < y) * y
MINIMUM = lambda x, y: (x > y) * y + (x < y) * x

a = 10
b = 20
print('The larger one is %d' % MAXIMUM(a, b))
print('The lower one is %d' % MINIMUM(a, b))


```

### 3) 效果
```
The larger one is 20
The lower one is 10
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
