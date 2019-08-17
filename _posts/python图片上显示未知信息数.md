---
title: 【第0000题】图片上显示未知消息数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
**第 0000 题：** 将你的 QQ 头像（或者微博头像）右上角加上红色的数字，类似于微信未读信息数量那种提示效果。 类似于图中效果

![](https://i.loli.net/2019/08/16/IxGN43jRudFUe2H.png)

# 题解
- 导入的三个包Image(图片打开展示等功能), ImageFont(字体), ImageDraw(画笔)
- 字体 fontSize 必须是整数，否则会报错（请自行尝试）
- 相对路径需要把 **图片** 或者 **字体** 放在 **py文件** 同一目录下，绝对路径中的 **斜杠** 有时候需要转义

### 1.代码
```
# coding=utf-8
# 第 0000 题：将你的 QQ 头像（或者微博头像）右上角加上红色的数字，
# 类似于微信未读信息数量那种提示效果。 类似于图中效果

from PIL import Image, ImageFont, ImageDraw

def addNum(num, filePath):
    img = Image.open(filePath)
    width, heigt = img.size
    fontSize = int(heigt / 4)
    draw = ImageDraw.Draw(img)
    # 确定字体格式和字体大小(整数)
    # 字体和图片都在与py文件同一目录下（相对路径）, 也可以用绝对路径写（有时需要转义）
    ttFont = ImageFont.truetype('C:\\Windows\\Fonts\\arial.ttf', fontSize)
    # 确定显示的 位置，数字，颜色，字体
    draw.text((width - fontSize, 50), num, (255, 0, 0), ttFont)
    del draw
    img.save('qq_addNumber.jpg')
    img.show()


if __name__ == '__main__':
    addNum('3', 'qq.jpg')
```

### 2.效果
<figure class="half">
    <img src="https://i.loli.net/2019/08/16/x6Hn5BqpN7kJoaY.jpg">
    <img src="https://i.loli.net/2019/08/16/BsSiHIfzdYn1JOC.png">
</figure>


---
***参考：
[博客](https://blog.51cto.com/yucanghai/1715170)***
