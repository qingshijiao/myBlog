---
title: 【python实例43】模拟静态变量static

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
模仿静态变量(static)另一案例。
# 题解
## 1.
### 1) 程序分析
演示一个python作用域使用方法
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


class Num:
    nNum = 1

    def inc(self):
        self.nNum += 1
        print('nNum = %d' % self.nNum)


if __name__ == '__main__':
    nNum = 2
    inst = Num()
    for i in range(3):
        nNum += 1
        print('The nNum = %d' % nNum)
        inst.inc()

```

### 3) 效果
```
The nNum = 3
nNum = 2
The nNum = 4
nNum = 3
The nNum = 5
nNum = 4
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
