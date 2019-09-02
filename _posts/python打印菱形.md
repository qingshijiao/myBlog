---
title: 【python实例23】打印菱形

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
打印出如下图案（菱形）:
```
   *
  ***
 *****
*******
 *****
  ***
   *
```
# 题解
## 1.
### 1) 程序分析
先把图形分成两部分来看待，前四行一个规律，后三行一个规律，利用双重for循环，第一层控制行，第二层控制列。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


n = int(input('enter a number: '))
for i in range(1, n + 1, 2):
    k = (n - i) // 2
    print(' ' * k, '*' * i)

for j in range(n - 2, 0, -2):
    m = (n - j) // 2
    print(' ' * m, '*' * j)

```

### 3) 效果
```
enter a number: 7
    *
   ***
  *****
 *******
  *****
   ***
    *
```

## 2.
### 1) 程序分析
从空格数量 3 2 1 0 1 2 3 我们可以看出，如果我们用公式求 k = (n - i) // 2 当 i 遍历到 7 时，k = 0， i 遍历到 9 时， k = -1，这时我们对 k 取绝对值，变为 k = 1 为空格数量。如下表，k 的绝对值为空格数量
i|k|abs(k)
--|--|:--:
1|3|3
3|2|2
5|1|1
7|0|0
9|-1|1
11|-2|2
13|-3|3

**说明：** 由于遍历范围不同，代码中公式稍有不同，不过都是用绝对值
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def pic(lines):
    middle = lines // 2
    for i in range(1, lines + 1):
        space = abs(middle - i + 1)
        print(' ' * space, '*' * (2 * (middle - space) + 1))


pic(7)

```

### 3) 效果
```
    *
   ***
  *****
 *******
  *****
   ***
    *
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
