---
title: 【第0022题】复用iphone图片

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0021 题：** 通常，登陆某个网站或者 APP，需要使用用户名和密码。密码是如何加密后存储起来的呢？请使用 Python 对密码加密。

- 阅读资料 [用户密码的存储与 Python 示例](http://zhuoqiang.me/password-storage-and-python-example.html)

- 阅读资料 [Hashing Strings with Python](http://www.pythoncentral.io/hashing-strings-with-python/)

- 阅读资料 [Python's safest method to store and retrieve passwords from a database](http://stackoverflow.com/questions/2572099/pythons-safest-method-to-store-and-retrieve-passwords-from-a-database)

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import os
from PIL import Image

PHONE = {'iPhone5': (1136, 640), 'iPhone6': (1134, 750), 'iPhone6P': (2208, 1242)}


def resize_pic(path, new_path, phone_type):
    im = Image.open(path)
    w, h = im.size

    width, height = PHONE[phone_type]

    if w > width:
        h = width * h // w
        w = width
    if h > height:
        w = height * w // h
        h = height

    im_resized = im.resize((w, h), Image.ANTIALIAS)
    im_resized.save(new_path)


def walk_dir_and_resize(path, phone_type):
    for root, dirs, files in os.walk(path):
        for f_name in files:
            if f_name.lower().endswith('jpg'):
                path_dst = os.path.join(root, f_name)
                # 新路径
                f_new_name = '..\\photo\\' + phone_type + '_' + f_name
                resize_pic(path=path_dst, new_path=f_new_name, phone_type=phone_type)


if __name__ == '__main__':
    walk_dir_and_resize('..\\photo', 'iPhone6')

```

---
***参考：
[shifanfashi](https://blog.csdn.net/shifanfashi/article/details/89512204)***
