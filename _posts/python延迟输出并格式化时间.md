---
title: 【python实例10】延迟输出并格式化时间

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
暂停一秒输出，并格式化当前时间。

# 题解
## 1.
### 1) 程序分析
使用 time 模块的 sleep() 函数。

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import time

print(time.strftime('%Y-%m-%d %H-%M-%S',time.localtime(time.time())))

# pause for one second
time.sleep(1)

print(time.strftime('%Y-%m-%d %H-%M-%S',time.localtime(time.time())))

```

### 3) 效果
```
2019-08-31 14-55-10
2019-08-31 14-55-11
```

## 2.
### 1) 程序分析
使用 time, datetime

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import datetime
import time

time.sleep(1)
TIME = datetime.datetime.now()
print(TIME.strftime('%Y-%m-%d %H-%M-%S'))

```
### 3) 效果
```
2019-08-31 14-57-34
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
