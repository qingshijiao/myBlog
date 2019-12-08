---
title: 【第0010题】字母验证图片

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0010 题：** 使用 Python 生成类似于下图中的**字母验证码图片**

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import random
import string
from PIL import Image, ImageFont, ImageDraw, ImageFilter  # pip3 install Pillow


def get_char():
    """
    生成随机字母
    """
    return random.choice(string.ascii_letters)


def generator_font_color():
    """
    生成随机字体颜色
    """
    return (random.randint(32, 255), random.randint(32, 255), random.randint(32, 255))


def generator_bgcolor():
    """
    生成随机背景颜色
    """
    return (random.randint(64, 355), random.randint(64, 355), random.randint(64, 355))


def imag_produce():
    w = 60 * 4
    h = 60
    img = Image.new('RGB', (w, h), (255, 255, 255))  # 生成一张新图片
    font = ImageFont.truetype('"C:\\WINDOWS\\Fonts\\SIMYOU.TTF', 60)  # 第一个参数为字体文件，第二个参数为字体大小
    draw = ImageDraw.Draw(img)  # 相当于生成一个画笔
    for i in range(w):  # 画背景，每个点的颜色随机
        for j in range(h):
            draw.point((i, j), fill=generator_bgcolor())
    for i in range(4):  # 画四个字母，每个字母颜色随机
        draw.text((i * 60 + 10, 10), get_char(), font=font, fill=generator_font_color())
    img.save('0010.jpg')


if __name__ == '__main__':
    imag_produce()

```

### 2) 效果
![](https://i.loli.net/2019/12/08/tR9BfkLhJGz7U5i.jpg)



---
***参考：
[m笑忘书](https://blog.csdn.net/qq_24822271/article/details/102609456)***
