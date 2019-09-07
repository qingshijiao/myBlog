---
title: 【python实例73】反向输出一个链表

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
反向输出一个链表。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

l = []
for i in range(5):
    l.append(int(input('input a number: ')))
print(l)

a = l[::-1]
print(a)

l.reverse()
print(l)

```

### 3) 效果
```
input a number: 1
input a number: 2
input a number: 3
input a number: 4
input a number: 5
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
[5, 4, 3, 2, 1]
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
