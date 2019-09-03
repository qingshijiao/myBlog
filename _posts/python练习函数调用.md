---
title: 【python实例34】练习函数调用

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
练习函数调用。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def hello_world():
    print('hello world')


def three_hellos():
    for i in range(3):
        hello_world()


if __name__ == '__main__':
    three_hellos()


```

### 3) 效果
```
hello world
hello world
hello world
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
