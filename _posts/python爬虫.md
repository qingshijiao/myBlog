---
title: 【第0013题】爬虫

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0013 题：** 用 Python 写一个爬图片的程序，爬 [这个链接里的日本妹子图片 :-)](http://tieba.baidu.com/p/2166231880)

- [参考代码](http://www.v2ex.com/t/61686 "参考代码")

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

from urllib import request
import re


def get_pic():
    """获取网页图片"""
    html = request.urlopen(r'http://tieba.baidu.com/p/2166231880')
    # 获取 html 内容
    page = html.read().decode()
    # 根据正则表达式匹配图片
    regex = re.compile(r'<img.*?class="BDE_Image" src="(.*?)".*?>')
    pic = re.findall(regex, page)
    return pic


def save(save_pic):
    """保存图片"""
    path = '..\\photo'
    count = 0
    for pic in save_pic:
        # 将远程图片下载到本地
        request.urlretrieve(pic, '%s/%s.jpg' % (path, count))
        count += 1


if __name__ == '__main__':
    pic = get_pic()
    save(pic)

```



---
***参考：
[fat_summer](https://blog.csdn.net/fat_summer/article/details/79157564)***
