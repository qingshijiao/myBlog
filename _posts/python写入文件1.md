---
title: 【python实例98】写入文件1

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
从键盘输入一个字符串，将小写字母全部转换成大写字母，然后输出到一个磁盘文件"test"中保存。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from sys import stdout

fp = open('test.txt', 'w')
string = input('please input a string:\n')
string = string.upper()
fp.write(string)
fp = open('test.txt', 'r')
print(fp.read())
fp.close()

```

### 3) 效果
```
please input a string:
abc
ABC

```
![](https://i.loli.net/2019/09/09/xcYD8TvlkP2qyCU.png)



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
