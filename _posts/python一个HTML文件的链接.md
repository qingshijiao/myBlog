---
title: 【第0009题】一个HTML文件的链接

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0009 题：** 一个HTML文件，找出里面的**链接**。

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


def get_href():
    soup = BeautifulSoup(html_doc, 'html.parser')
    a_tags = soup.find_all('a')

    href_list = []
    for a_tag in a_tags:
        href = a_tag.get('href')
        if href:
            a_tag.get('href')
            href_list.append(href)
    print(href_list)
    return href_list


if __name__ == '__main__':
    get_href()

```

### 2) 效果

```
['http://example.com/elsie', 'http://example.com/lacie', 'http://example.com/tillie']
```



---
***参考：
[简书](https://www.jianshu.com/p/84ea52bbdf3a)***
