---
title: 【第0001题】生成激活码

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目

**第 0001 题：** 作为 Apple Store App 独立开发者，你要搞限时促销，为你的应用**生成激活码**（或者优惠券），使用 Python 如何生成 200 个激活码（或者优惠券）？

# 题解
## 1.

### 1)代码
```

# -*- coding: utf-8 -*-
import uuid


# 生成 num 个验证码，每个长度为length，可设置默认长度
def create_num(num, length=16):
    result = []
    while num > 0:
        uuid_id = uuid.uuid1()
        # 删去字符串中的'-',取出前length 个字符
        temp = str(uuid_id).replace('-', '')[:length]
        if temp not in result:
            result.append(temp)
            num -= 1
    return result

if __name__ == '__main__':
  print(create_num(200, 32))
  print(create_num(200))
```

### 2)效果
> 32长度：'1da7b036c09a11e981cf6014b3b7db4c'
> 16长度：'1da9ab1ac09a11e9'

### 3)说明
UUID是128位的全局唯一标识符，通常由32字节的字符串表示。它可以保证时间和空间的唯一性，也称为GUID，全称为：UUID —— Universally Unique IDentifier，Python 中叫 UUID。

它通过MAC地址、时间戳、命名空间、随机数、伪随机数来保证生成ID的唯一性。
UUID主要有五个算法，也就是五种方法来实现。

- uuid1()——基于时间戳。由MAC地址、当前时间戳、随机数生成。可以保证全球范围内的唯一性，但MAC的使用同时带来安全性问题，局域网中可以使用IP来代替MAC。
- uuid2()——基于分布式计算环境DCE（Python中没有这个函数）。算法与uuid1相同，不同的是把时间戳的前4位置换为POSIX的UID。实际中很少用到该方法。
- uuid3()——基于名字的MD5散列值。通过计算名字和命名空间的MD5散列值得到，保证了同一命名空间中不同名字的唯一性，和不同命名空间的唯一性，但同一命名空间的同一名字生成相同的uuid。
- uuid4()——基于随机数。由伪随机数得到，有一定的重复概率，该概率可以计算出来。
- uuid5()——基于名字的SHA-1散列值。算法与uuid3相同，不同的是使用 Secure Hash Algorithm 1 算法。

## 2.
### 1)代码
```
#!/usr/bin/env python
# coding: utf-8
import random
import string

# 激活码中的字符和数字
field = string.ascii_letters + string.digits


# 获得四个字母和数字的随机组合
def getRandom():
    return "".join(random.sample(field, 4))


# 生成的每个激活码中有几组
def concatenate(group):
    return "-".join([getRandom() for i in range(group)])


# 生成n组激活码
def generate(n):
    return [concatenate(4) for i in range(n)]


if __name__ == '__main__':
    print(generate(200))

```
### 2)效果
> 'Tk5X-Fi0S-BmFe-LIY6'



---
***参考：
[博客](https://blog.51cto.com/yucanghai/1715170)***
