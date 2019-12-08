---
title: 【第0016题】文本转表格3

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目
**第 0016 题：** 纯文本文件 numbers.txt, 里面的内容（包括方括号）如下所示：

    [
    	[1, 82, 65535],
    	[20, 90, 13],
    	[26, 809, 1024]
    ]

请将上述内容写到 numbers.xls 文件中，如下图所示：

![numbers.xls](http://i.imgur.com/iuz0Pbv.png)

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import json
import xlwt


def read_text():
    with open("..\\text\\numbers.txt", encoding='UTF-8') as f:
        return f.read()


def write_excel(infos: dict):
    workbook = xlwt.Workbook()
    worksheet = workbook.add_sheet('numbers')

    for row_index, row in enumerate(infos):
        for column_index, column_value in enumerate(row):
            worksheet.write(row_index, column_index, label=column_value)

    workbook.save("..\\text\\numbers.xls")


if __name__ == "__main__":
    text = read_text()
    infos = json.loads(text)
    print(infos)
    write_excel(infos)

```

### 2) 效果

![](https://i.loli.net/2019/12/08/LUhZyqPjxBGmFwV.jpg)

---
***参考：
[Sesshoumaru](https://github.com/Sesshoumaru/python-exercise/blob/master/0016/0016.py)***
