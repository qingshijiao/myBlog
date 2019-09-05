---
title: 【python实例55】按位取反

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
学习使用按位取反~。
# 题解
## 1.
### 1) 程序分析
~0=1; ~1=0;
**说明：**
- 按位中的位是补码的位，取反后仍为补码。
- 补码 -按位取反-> -末位加 1 -> 原码

[按位取反运算](http://www.51testing.com/html/07/84407-1074717.html)

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = 234
b = ~a
print('The a\'s 1 complement is %d' % b)
a = ~a
print('The a\'s 2 complement is %d' % a)

```

### 3) 效果
```
The a's 1 complement is -235
The a's 2 complement is -235
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
