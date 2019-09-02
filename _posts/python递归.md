---
title: 【python实例26】递归

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
利用递归方法求5!。
# 题解
## 1.
### 1) 程序分析
递归公式：fn=fn_1*4!
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def fact(n):
    if n == 0:
        return 1
    else:
        return n * fact(n - 1)


print(fact(5))

```

### 3) 效果
```
120
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
