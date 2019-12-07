---
title: 【第0008题】一个HTML文件的正文

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0008 题：** 一个HTML文件，找出里面的**正文**。

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

from bs4 import BeautifulSoup

html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""


def get_content():
    soup = BeautifulSoup(html_doc, 'html.parser')
    contents = soup.select('p.story')

    result = ''
    for content in contents:
        result += content.get_text()
    print(result)
    return result


if __name__ == '__main__':
    get_content()

```

### 2) 效果

```
Once upon a time there were three little sisters; and their names were
Elsie,
Lacie and
Tillie;
and they lived at the bottom of a well....
```



---
***参考：
[简书](https://www.jianshu.com/p/84ea52bbdf3a)***
