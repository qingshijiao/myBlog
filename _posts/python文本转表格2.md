---
title: 【第0015题】文本转表格2

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0015 题：** 纯文本文件 city.txt为城市信息, 里面的内容（包括花括号）如下所示：

    {
        "1" : "上海",
        "2" : "北京",
        "3" : "成都"
    }

请将上述内容写到 city.xls 文件中，如下图所示：

![city.xls](http://i.imgur.com/rOHbUzg.png)

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import json
import xlwt


def read_text():
    with open("..\\text\\city.txt", encoding='UTF-8') as f:
        return f.read()


def write_excel(infos: dict):
    workbook = xlwt.Workbook() # 工作簿
    worksheet = workbook.add_sheet('city') # 工作表

    row = 0
    for k in sorted(infos.keys()):
        worksheet.write(row, 0, label=k)
        worksheet.write(row, 1, label=infos[k])
        row += 1 # 行

    workbook.save("..\\text\\city.xls")


if __name__ == "__main__":
    text = read_text()
    infos = json.loads(text)
    print(infos)
    write_excel(infos)

```

### 2) 效果

![](https://i.loli.net/2019/12/08/djrnfueR3bQm58v.jpg)


---
***参考：
[Sesshoumaru](https://github.com/Sesshoumaru/python-exercise/blob/master/0015/0015.py)***
