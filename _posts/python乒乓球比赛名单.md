---
title: 【python实例22】乒乓球比赛名单

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
两个乒乓球队进行比赛，各出三人。甲队为a,b,c三人，乙队为x,y,z三人。已抽签决定比赛名单。有人向队员打听比赛的名单。a说他不和x比，c说他不和x,z比，请编程序找出三队赛手的名单。

# 题解
## 1.
### 1) 程序分析

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


for a in ['x', 'y', 'z']:
    for b in ['x', 'y', 'z']:
        for c in ['x', 'y', 'z']:
            if (a != b) and (b != c) and (c != a) \
                    and (a != 'x') and (c != 'x') and (c != 'z'):
                print('order is a -- %s\t b -- %s\t c -- %s' % (a, b, c))


```

### 3) 效果
```
order is a -- z	 b -- x	 c -- y
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
