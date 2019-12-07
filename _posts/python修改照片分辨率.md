---
title: 【第0005题】修改照片分辨率

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0005 题：** 你有一个目录，装了很多照片，把它们的尺寸变成都不大于 iPhone5 分辨率的大小。

# 题解
## 1.

### 1)代码
```
import os
from PIL import Image

# 文件目录
path_dir = 'E:\VirtualDesktop\code\pyCode\Test\photo'


# 修改图片尺寸
def modify_imgsize():
    # 遍历得到的图片
    for file_name in get_img_list(path_dir):
        # 打开图片
        img = Image.open(path_dir + '\\' + file_name)
        if max(img.size) > 1136: # 图片分辨率不符合标准则修改
            # 得到最短边大小
            value = max(img.size) / 1136.0
            newsize_min = min(img.size) / value
            # 修改大小
            newimg = img.resize((1136, int(newsize_min)), Image.ANTIALIAS)
            # 保存图片
            newimg.save(path_dir + '\\' + 'new_' + file_name)
        else: # 图片分辨率符合
            print('This picture is available: ' + file_name)


# 获取图片名称
def get_img_list(path_dir):
    img_list = []
    list_dir = os.listdir(path_dir)
    for x in list_dir:
        if '.jpg' in x:
            img_list.append(x)
        elif '.png' in x:
            img_list.append(x)
        else:
            print(x + ' is not a picture')
    return img_list


if __name__ == '__main__':
    modify_imgsize()

```



---
***参考：
[no_giveup](https://blog.csdn.net/no_giveup/article/details/51348314)***
