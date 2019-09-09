---
title: 【python实例94】时间函数4

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
时间函数举例4。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-
import time
import random

start = time.time()
while True:
    play = input('play the game(y/n)?')
    if play == 'y':
        number = random.randint(0, 1000)
        guess = int(input('guess a number: '))
        while True:
            if number > guess:
                guess = int(input("guess a bigger number: "))
            elif number < guess:
                guess = int(input("guess a smaller number: "))
            else:
                end = time.time()
                print("bingo! ")
                print(u"%0.2fs猜中" % (end - start))
                break
    else:
        break

```

### 3) 效果
```
play the game(y/n)?y
guess a number: 50
guess a bigger number: 100
guess a bigger number: 1000
guess a smaller number: 500
guess a bigger number: 750
guess a smaller number: 600
guess a bigger number: 650
guess a bigger number: 700
guess a smaller number: 675
guess a smaller number: 660
guess a bigger number: 670
guess a smaller number: 666
guess a bigger number: 668
bingo!
51.64s猜中
play the game(y/n)?n
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
