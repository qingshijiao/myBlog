---
title: 【python实例14】整数分解质因数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
将一个正整数分解质因数。例如：输入 90,打印出90 = 2 * 3 * 3 * 5。

# 题解
## 1.
### 1) 程序分析
对n进行分解质因数，应先找到一个最小的质数k，然后按下述步骤完成：
- 如果这个质数恰等于n，则说明分解质因数的过程已经结束，打印出即可。
- 如果n>k，但n能被k整除，则应打印出k的值，并用n除以k的商,作为新的正整数你n,重复执行第一步。
- 如果n不能被k整除，则用k+1作为k的值,重复执行第一步。　　　

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def reduceNum(n):
    print('{} = '.format(n))
    if not isinstance(n, int) or n <= 0:
        print('please enter a correct number: ')
        # after this code will not execute, no error exit
        exit(0)
    elif n in [1]:
        print('{}'.format(n))
    while n not in [1]:
        for index in range(2, n + 1):
            if n % index == 0:
                n = int(n / index)
                if n == 1:
                    print(index)
                else:
                    print('{} * '.format(index), end='')
                break


reduceNum(90)
reduceNum(100)

```

### 3) 效果
```
90 =
2 * 3 * 3 * 5
100 =
2 * 2 * 5 * 5
```

## 2.
### 1) 程序分析

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def reduceNum():
    n = int(input('please enter a number: '))
    if not isinstance(n, int) or n <= 0:
        print('please enter a correct number: ')
    i = 2
    print('%d = ' % n, end='')
    if n != 1:
        while i != n:
            if n % i == 0:
                print('%d * ' % i, end='')
                n = n // i
            else:
                i += 1
        print(i)
    else:
        print(n)


reduceNum()
reduceNum()

```
**说明：** python 3.x 中 // 表示取整

### 3) 效果
```
please enter a number: 90
90 = 2 * 3 * 3 * 5
please enter a number: 100
100 = 2 * 2 * 5 * 5
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
