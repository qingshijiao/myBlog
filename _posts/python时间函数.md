---
title: 【python实例91】时间函数1

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
时间函数举例1。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


import time

print(time.ctime(time.time()))
print(time.asctime(time.localtime(time.time())))
print(time.asctime(time.gmtime(time.time())))


```

### 3) 效果
```
Mon Sep  9 13:12:54 2019
Mon Sep  9 13:12:54 2019
Mon Sep  9 05:12:54 2019
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
