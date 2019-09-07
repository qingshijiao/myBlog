---
title: 【python实例76】奇偶输出公式

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
编写一个函数，输入n为偶数时，调用函数求1/2+1/4+...+1/n,当输入n为奇数时，调用函数1/1+1/3+...+1/n

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def peven(n):
    i = 0
    s = 0.0
    for i in range(2, n + 1, 2):
        s += 1.0 / i
    return s


def podd(n):
    i = 0
    s = 0.0
    for i in range(1, n + 1, 2):
        s += 1.0 / i
    return s


def dcall(fp, n):
    return fp(n)


if __name__ == '__main__':
    n = int(input('input a number: '))
    if n % 2 == 0:
        print(dcall(peven, n))
    else:
        print(dcall(podd, n))

```

### 3) 效果
```
input a number: 6
0.9166666666666666
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
