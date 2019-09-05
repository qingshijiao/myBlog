---
title: 【python实例51】按位与

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
学习使用按位与 & 。
# 题解
## 1.
### 1) 程序分析
0&0=0; 0&1=0; 1&0=0; 1&1=1。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

# 二进制
a = 0b11
b = a & 3
print('a & b = %d' % b)
b &= 1
print('a & b = %d' % b)

```

### 3) 效果
```
a & b = 3
a & b = 1
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
