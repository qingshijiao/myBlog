---
title: 【python实例66】大小排序2

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入3个数a,b,c，按大小顺序输出。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n1 = int(input('n1 = :\n'))
n2 = int(input('n2 = :\n'))
n3 = int(input('n3 = :\n'))

if n1 > n2:
    n1, n2 = n2, n1
if n1 > n3:
    n1, n3 = n3, n1
if n2 > n3:
    n2, n3 = n3, n2

print(n1, n2, n3)

```

### 3) 效果
```
n1 = :
2
n2 = :
3
n3 = :
1
1 2 3
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
