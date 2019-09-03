---
title: 【python实例35】文本颜色设置

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
文本颜色设置.
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


class Colors:
    HEADER = '\033[95m'
    OKBULE = '\033[94m'
    OKGREEN = '\033[92m'
    WARNING = '\033[93m'
    FAIL = '\033[91m'
    ENDC = '\033[0m'
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'


print(Colors.WARNING + '警告的颜色字体？' + Colors.ENDC)
print(Colors.HEADER + 'HEADER')
print(Colors.OKBULE + 'OKBULE')
print(Colors.OKGREEN + 'OKGREEN')
print(Colors.WARNING + 'WARNING')
print(Colors.FAIL + 'FAIL')
print(Colors.ENDC + 'ENDC')
print(Colors.BOLD + 'BOLD')
print(Colors.UNDERLINE + 'UNDERLINE')

```

### 3) 效果
![](https://i.loli.net/2019/09/03/pzRMds7chlU9jrQ.png)


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
