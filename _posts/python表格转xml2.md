---
title: 【第0018题】表格转xml2

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目
**第 0018 题：** 将 第 0015 题中的 city.xls 文件中的内容写到 city.xml 文件中，如下所示：
```
<?xmlversion="1.0" encoding="UTF-8"?>
<root>
   <cities>
<!--
	城市信息
-->
{
	"1" : "上海",
	"2" : "北京",
	"3" : "成都"
}
</cities>
</root>
```


# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-


def read_excel():
    import xlrd
    with xlrd.open_workbook("..\\text\\city.xls") as f:
        sheet = f.sheet_by_index(0)
        row_count = sheet.nrows
        column_count = sheet.ncols
        result = {}
        for row in range(row_count):
            id = sheet.cell(row, 0).value
            values = []
            for column in range(1, column_count):
                values.append(sheet.cell(row, column).value)

            result[id] = values
        return result


def wirte_xml(infos):
    import xml.dom.minidom
    import json

    impl = xml.dom.minidom.getDOMImplementation()
    dom = impl.createDocument(None, 'root', None)
    root = dom.documentElement
    stduent = dom.createElement("citys")
    comment = dom.createComment('城市信息')
    stduent.appendChild(comment)

    josn_text = json.dumps(infos, ensure_ascii=False)
    print(josn_text)
    text = dom.createCDATASection(josn_text)
    stduent.appendChild(text)
    root.appendChild(stduent)
    print(dom.toprettyxml())

    f = open('..\\text\\city.xml', 'w', encoding='utf-8')
    dom.writexml(f, addindent='', newl='', encoding='utf-8')


if __name__ == "__main__":
    infos = read_excel()
    wirte_xml(infos)

```

### 2) 效果

```
<?xml version="1.0" encoding="utf-8"?><root><citys><!--城市信息--><![CDATA[{"1": ["上海"], "2": ["北京"], "3": ["成都"]}]]></citys></root>
```

---
***参考：
[Sesshoumaru](https://github.com/Sesshoumaru/python-exercise/blob/master/0018/0018.py)***
