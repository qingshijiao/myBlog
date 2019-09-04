---
title: 【python实例46】求输入数字的平方

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求输入数字的平方，如果平方运算后小于 50 则退出。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

TRUE = 1
FALSE = 0


def sq(x):
    return x * x


print('如果输入的数字小于 50，程序将停止运行。')
again = 1
while again:
    num = int(input('请输入一个数字：'))
    print('运算结果为: %d' % (sq(num)))
    if sq(num) >= 50:
        again = TRUE
    else:
        again = FALSE


```

### 3) 效果
```
如果输入的数字小于 50，程序将停止运行。
请输入一个数字：12
运算结果为: 144
请输入一个数字：5
运算结果为: 25
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
