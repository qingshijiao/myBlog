---
title: 【第0017题】表格转xml1

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目
**第 0017 题：** 将 第 0014 题中的 student.xls 文件中的内容写到 student.xml 文件中，如下所示：
```
<?xml version="1.0" encoding="UTF-8"?>
<root>
<students>
<!--
	学生信息表
	"id" : [名字, 数学, 语文, 英文]
-->
{
	"1" : ["张三", 150, 120, 100],
	"2" : ["李四", 90, 99, 95],
	"3" : ["王五", 60, 66, 68]
}
</students>
</root>
```


# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import xlrd
import json
import xml.dom.minidom


def read_excel():
    with xlrd.open_workbook("..\\text\\student.xls") as f:
        sheet = f.sheet_by_index(0)
        row_count = sheet.nrows
        column_count = sheet.ncols
        result = {}
        for row in range(row_count):
            id = sheet.cell(row, 0).value  # sheet.cell().value 获取单元格内容
            values = []
            for column in range(1, column_count):
                values.append(sheet.cell(row, column).value)

            result[id] = values
        return result


def wirte_xml(infos):
    impl = xml.dom.minidom.getDOMImplementation()
    dom = impl.createDocument(None, 'root', None)
    root = dom.documentElement
    stduent = dom.createElement("students")
    comment = dom.createComment('''
    学生信息表
    "id" : [名字, 数学, 语文, 英文]
    ''')
    stduent.appendChild(comment)

    josn_text = json.dumps(infos, ensure_ascii=False)
    print(josn_text)
    text = dom.createCDATASection(josn_text)
    stduent.appendChild(text)
    root.appendChild(stduent)
    print(dom.toprettyxml())

    f = open('..\\text\\student.xml', 'w', encoding='utf-8')
    dom.writexml(f, addindent='', newl='', encoding='utf-8')


if __name__ == "__main__":
    infos = read_excel()
    wirte_xml(infos)

```

### 2) 效果

```
<?xml version="1.0" encoding="utf-8"?><root><students><!--
    学生信息表
    "id" : [名字, 数学, 语文, 英文]
    --><![CDATA[{"1": ["张三", 150.0, 120.0, 100.0], "2": ["李四", 90.0, 99.0, 95.0], "3": ["王五", 60.0, 66.0, 68.0]}]]></students></root>
```

---
***参考：
[Sesshoumaru](https://github.com/Sesshoumaru/python-exercise/blob/master/0017/0017.py)***
