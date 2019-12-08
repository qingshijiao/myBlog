---
title: 【第0014题】文本转表格1

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0014 题：** 纯文本文件 student.txt为学生信息, 里面的内容（包括花括号）如下所示：

    {
    	"1":["张三",150,120,100],
    	"2":["李四",90,99,95],
    	"3":["王五",60,66,68]
    }

请将上述内容写到 student.xls 文件中，如下图所示：

![student.xls](http://i.imgur.com/nPDlpme.jpg)

- [阅读资料](http://www.cnblogs.com/skynet/archive/2013/05/06/3063245.html) 腾讯游戏开发 XML 和 Excel 内容相互转换

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import json
import xlwt
from collections import OrderedDict


def build():
    with open('..\\text\\student.txt', encoding='utf-8') as f:
        # 根据 json 格式加载为字典
        students_dict = OrderedDict(json.load(f))
        # print(students_dict)

    wb = xlwt.Workbook()  # 创建一个工作簿
    ws = wb.add_sheet('student')  # 创建一个sheet

    row = 0 # 行
    for k, v in students_dict.items():
        ws.write(row, 0, k)
        col = 1 # 列
        for item in v:
            ws.write(row, col, item)
            col += 1
        row += 1
    wb.save('..\\text\\student.xls')  # 保存


if __name__ == '__main__':
    build()

```

### 2) 效果

![](https://i.loli.net/2019/12/08/w4OyTK6ozIu3t7E.jpg)



---
***参考：
[wanlifeipeng](https://www.cnblogs.com/hupeng1234/p/6681800.html)***
