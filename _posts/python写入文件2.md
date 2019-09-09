---
title: 【python实例99】写入文件2

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有两个磁盘文件A和B,各存放一行字母,要求把这两个文件中的信息合并(按字母顺序排列), 输出到一个新文件C中。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
from sys import stdout

import string

fp = open('test1.txt')
a = fp.read()
fp.close()

fp = open('test2.txt')
b = fp.read()
fp.close()

fp = open('test3.txt', 'w')
l = list(a + b)
l.sort()
s = ''
s = s.join(l)
fp.write(s)
fp.close()


```

### 3) 效果
```

```
![](https://i.loli.net/2019/09/09/kjuTeLzAwsDtcbU.png)
![](https://i.loli.net/2019/09/09/kTpRPeIwj12lcCx.png)



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
