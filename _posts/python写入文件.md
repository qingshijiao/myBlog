---
title: 【python实例97】写入文件

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
从键盘输入一些字符，逐个把它们写到磁盘文件上，直到输入一个 # 为止。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from sys import stdout

filename = input('输入文件名:\n')
fp = open(filename, "w")
ch = input('输入字符串:\n')
while ch != '#':
    fp.write(ch)
    stdout.write(ch)
    ch = input('')
fp.close()

```

### 3) 效果
```
输入文件名:
text.txt
输入字符串:
abc
abcabcde
abcdea#
a#
#

```
![](https://i.loli.net/2019/09/09/hQyiTGYlIwtdmRx.png)
![](https://i.loli.net/2019/09/09/5KTX1JbV4ZkQNBG.png)


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
