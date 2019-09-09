---
title: 【python实例93】时间函数3

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
时间函数举例3。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import time

start = time.clock()
for i in range(10000):
    print(i)

end = time.clock()
print('different is %6.3f' % (end - start))


```

### 3) 效果
```
...
9991
9992
9993
9994
9995
9996
9997
9998
9999
different is  0.095
E:/Virtual Desktop/code/pyCode/Exercise/test.py:9: DeprecationWarning: time.clock has been deprecated in Python 3.3 and will be removed from Python 3.8: use time.perf_counter or time.process_time instead
  end = time.clock()
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import time

start = time.perf_counter()
for i in range(10000):
    print(i)

end = time.perf_counter()
print('different is %6.3f' % (end - start))


```

### 3) 效果
```
...
9991
9992
9993
9994
9995
9996
9997
9998
9999
different is  0.094
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
