---
title: 【python实例80】猴子拿桃

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
海滩上有一堆桃子，五只猴子来分。第一只猴子把这堆桃子平均分为五份，多了一个，这只猴子把多的一个扔入海中，拿走了一份。第二只猴子把剩下的桃子又平均分成五份，又多了一个，它同样把多的一个扔入海中，拿走了一份，第三、第四、第五只猴子都是这样做的，问海滩上原来最少有多少个桃子？
# 题解
## 1.
### 1) 程序分析
反向思考，从剩余桃数入手
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


i = 0
j = 1
while i < 5:
    x = 4 * j  # 剩余桃数 4 8 12 ...
    for i in range(0, 5):
        if x % 4 != 0:
            break
        else:
            i += 1
        x = (x / 4) * 5 + 1
    j += 1
print(x)

```

### 3) 效果
```
3121.0
```

## 2.
### 1) 程序分析
正向思考，从总桃数，程序的顺序稍有不同
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

cout = 0
j = 1
t = 0
while cout < 5:
    t = j * 5 + 1
    x = t
    cout = 0
    for i in range(0, 5):
        x = (x - 1) / 5 * 4
        if x % 4 != 0:
            break
        else:
            cout += 1
    j += 1
print(t)

```

### 3) 效果
```
3121
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
