---
title: 【python实例81】四位数分解

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
809 * ??=800 * ??+9 * ?? 其中??代表的两位数, 809 * ??为四位数，8*??的结果为两位数，9*??的结果为3位数。求??代表的两位数，及809*??后的结果

# 题解
## 1.
### 1) 程序分析

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = 809
for i in range(10,100):
    b = i * a
    if (1000 <= b <= 10000) and (8 * i < 100) and (9 * i >= 100):
        print(b, ' = 800 * ', i, ' + 9 * ', i)

```

### 3) 效果
```
9708  = 800 *  12  + 9 *  12
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
