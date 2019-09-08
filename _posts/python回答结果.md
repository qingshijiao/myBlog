---
title: 【python实例87】回答结果

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
回答结果（结构体变量传递）。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


class Student:
    x = 0
    c = 0


def f(stu):
    stu.x = 20
    stu.c = 'c'


a = Student()
a.x = 3
a.c = 'a'
f(a)
print(a.x, a.c)

```

### 3) 效果
```
20 c
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
