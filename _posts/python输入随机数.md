---
title: 【python实例50】输出一个随机数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输出一个随机数。
# 题解
## 1.
### 1) 程序分析
使用 random 模块。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import random

print(random.random())  # 输入0-1之间的随机数
print(random.uniform(10, 20))  # 输出10-20之间的随机数
print(random.randint(10, 20))  # 输出10-20之间的随机整数

```

### 3) 效果
```
0.5373854290042059
13.442935110958324
16
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
