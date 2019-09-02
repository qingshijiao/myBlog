---
title: 【python实例30】判断数字是否为回文数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
一个5位数，判断它是不是回文数。即12321是回文数，个位与万位相同，十位与千位相同。
# 题解
## 1.
### 1) 程序分析
将数字前一半部分反转，和后一半部分相比
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = int(input('enter a number: '))
n = a
t = 0
for i in range(len(str(n)) // 2):
    t = t * 10 + n % 10
    n = n // 10

if (t == n) or (t == n // 10):
    print('%s is palindromic number' % a)
else:
    print('%s is not palindromic number' % a)

```

### 3) 效果
```
enter a number: 12321
12321 is palindromic number
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = input('enter a number: ')
b = a[::-1]
if a == b:
    print('%s is palindromic number' % a)
else:
    print('%s is not palindromic number' % a)

```

### 3) 效果
```
enter a number: 12321
12321 is palindromic number
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
