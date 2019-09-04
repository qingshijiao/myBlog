---
title: 【python实例47】两个变量值互换

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
两个变量值互换。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def exchange(a, b):
    a, b = b, a
    return a, b


x = 10
y = 20
print('x = %d, y = %d' % (x, y))
x, y = exchange(x, y)
print('x = %d, y = %d' % (x, y))


```

### 3) 效果
```
x = 10, y = 20
x = 20, y = 10
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
