---
title: 【第0019题】表格转xml3

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目
**第 0019 题：** 将 第 0016 题中的 numbers.xls 文件中的内容写到 numbers.xml 文件中，如下所示：
```
<?xml version="1.0" encoding="UTF-8"?>
<root>
<numbers>
<!--
	数字信息
-->

[
	[1, 82, 65535],
	[20, 90, 13],
	[26, 809, 1024]
]

</numbers>
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
    with xlrd.open_workbook("..\\text\\numbers.xls") as f:
        sheet = f.sheet_by_index(0)
        row_count = sheet.nrows
        column_count = sheet.ncols
        result = []
        for row in range(row_count):
            values = []
            for column in range(0, column_count):
                values.append(sheet.cell(row, column).value)

            result.append(values)
        return result


def wirte_xml(infos):
    impl = xml.dom.minidom.getDOMImplementation()
    dom = impl.createDocument(None, 'root', None)
    root = dom.documentElement
    stduent = dom.createElement("numbers")
    comment = dom.createComment('数字信息')
    stduent.appendChild(comment)

    josn_text = json.dumps(infos, ensure_ascii=False)
    print(josn_text)
    text = dom.createCDATASection(josn_text)
    stduent.appendChild(text)
    root.appendChild(stduent)
    print(dom.toprettyxml())

    f = open('..\\text\\numbers.xml', 'w', encoding='utf-8')
    dom.writexml(f, addindent='', newl='', encoding='utf-8')


if __name__ == "__main__":
    infos = read_excel()
    wirte_xml(infos)

```

### 2) 效果

```
<?xml version="1.0" encoding="utf-8"?><root><numbers><!--数字信息--><![CDATA[[[1.0, 82.0, 65535.0], [20.0, 90.0, 13.0], [26.0, 809.0, 1024.0]]]]></numbers></root>
```

---
***参考：
[Sesshoumaru](https://github.com/Sesshoumaru/python-exercise/blob/master/0019/0019.py)***
