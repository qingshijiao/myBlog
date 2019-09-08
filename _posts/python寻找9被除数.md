---
title: 【python实例85】寻找9被除数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入一个奇数，然后判断最少几个 9 除于该数的结果为整数。

# 题解
## 1.
### 1) 程序分析
999999 / 13 = 76923。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

b = int(input('input a number:\n'))

a = 9
n = 1
while 1:
    if a % b == 0:
        break
    else:
        a = a * 10 + 9
        n = n + 1
print('%d 个 9 除于 %d 为整数' % (n, b))

```

### 3) 效果
```
input a number:
13
6 个 9 除于 13 为整数
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
