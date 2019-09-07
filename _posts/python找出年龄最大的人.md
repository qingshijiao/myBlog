---
title: 【python实例78】找出年龄最大的人

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
找到年龄最大的人，并输出。请找出程序中有什么问题。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


person = {"li": 18, "wang": 50, "zhang": 20, "sun": 22}
m = 'li'
for key in person.keys():
    if person[m] < person[key]:
        m = key

print('%s,%d' % (m, person[m]))


```

### 3) 效果
```
wang,50
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
