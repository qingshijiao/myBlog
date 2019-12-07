---
title: 【第0007题】代码行分类

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0007 题：** 有个目录，里面是你自己写过的程序，统计一下你写过多少行代码。包括空行和注释，但是要分别列出来。

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import os
import sys


def get_code_lines(input_path):
    """
    对文件夹中所有文件统计代码、空格、注释数量
    """
    if not os.path.isdir(input_path):
        print("input not directory!")
        sys.exit()
    os.chdir(input_path)
    count = {"code_num": 0, "space_num": 0, "comment_num": 0}
    for one_file in os.listdir(os.getcwd()):
        print(one_file)
        get_file_code_num(one_file, count)
    print(count)


def get_file_code_num(one_file, count):
    """
    统计文件中的代码、空格、注释的数量
    回车 \r 本义是光标重新回到本行开头
    空行中隐式包含'\n'，每行代码的结尾包含'\r\n'
    """
    if not os.path.isfile(one_file):
        print("is not file")
        sys.exit()
    for line in open(one_file, "r"):
        if ("#" in line) or ("\"\"\"" in line):
            count["comment_num"] += 1
        elif line == '\n':
            count["space_num"] += 1
        else:
            count["code_num"] += 1


if __name__ == '__main__':
    path = 'E:\\VirtualDesktop\\code\\pyCode\\Test\\text'
    get_code_lines(path)

```



---
***参考：
[Angelahhj](https://blog.csdn.net/Angelahhj/article/details/53318454)***
