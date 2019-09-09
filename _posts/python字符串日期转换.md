---
title: 【python实例95】字符串日期转换

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
字符串日期转换为易读的日期格式。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from dateutil import parser
dt = parser.parse("Aug 28 2015 12:00AM")
print(dt)

```

### 3) 效果
```
2015-08-28 00:00:00
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
