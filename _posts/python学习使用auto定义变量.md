---
title: 【python实例42】学习使用 auto 定义变量

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
学习使用auto定义变量的用法。
# 题解
## 1.
### 1) 程序分析
没有auto关键字，使用变量作用域来举例吧。全局变量和局部变量关系。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


num = 2


def autofunc():
    num = 1
    print('internal block num = %d' % num)
    num += 1


for i in range(3):
    print('The num = %d' % num)
    num += 1
    autofunc()

```

### 3) 效果
```
The num = 2
internal block num = 1
The num = 3
internal block num = 1
The num = 4
internal block num = 1
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
