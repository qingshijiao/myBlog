---
title: 【python实例17】统计字符的个数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入一行字符，分别统计出其中英文字母、空格、数字和其它字符的个数。

# 题解
## 1.
### 1) 程序分析
利用 while 语句,条件为输入的字符不为 '\n'。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import string

s = input('please enter a string: \n')
letters = 0
space = 0
digit = 0
others = 0
i = 0
while i < len(s):
    c = s[i]
    i += 1
    if c.isalpha():
        letters += 1
    elif c.isspace():
        space += 1
    elif c.isdigit():
        digit += 1
    else:
        others += 1

print('char = %d, space = %d, digit = %d, others = %d'
      % (letters, space, digit, others))

```

### 3) 效果
```
please enter a string:
123runoobc  kdf235*(dfl
char = 13, space = 2, digit = 6, others = 2
```
## 2.
### 1) 程序分析
利用 for 语句,条件为输入的字符不为 '\n'。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import string

s = input('please enter a string: \n')
letters = 0
space = 0
digit = 0
others = 0
for c in s:
    if c.isalpha():
        letters += 1
    elif c.isspace():
        space += 1
    elif c.isdigit():
        digit += 1
    else:
        others += 1

print('char = %d, space = %d, digit = %d, others = %d'
      % (letters, space, digit, others))


```

### 3) 效果
```
please enter a string:
123runoobc  kdf235*(dfl
char = 13, space = 2, digit = 6, others = 2
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
