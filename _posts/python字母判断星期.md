---
title: 【python实例31】字母判断星期

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
请输入星期几的第一个字母来判断一下是星期几，如果第一个字母一样，则继续判断第二个字母。
# 题解
## 1.
### 1) 程序分析
用情况语句比较好，如果第一个字母一样，则判断用情况语句或if语句判断第二个字母。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

letter = input('please input: ')
if letter == 'S':
    print('please input second letter: ')
    letter = input('please input: ')
    if letter == 'a':
        print('Saturday')
    elif letter == 'u':
        print('Sunday')
    else:
        print('data error')

elif letter == 'F':
    print('Friday')

elif letter == 'M':
    print('Monday')

elif letter == 'T':
    print('please input second letter: ')
    letter = input('please input: ')
    if letter == 'u':
        print('Tuesday')
    elif letter == 'h':
        print('Thursday')
    else:
        print('data error')

elif letter == 'W':
    print('Wednesday')

else:
    print('data error')


```

### 3) 效果
```
please input: T
please input second letter:
please input: h
Thursday
```

## 2.
### 1) 程序分析
用字典存储
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

weekList = {'M': 'Monday', 'T': {'u': 'Tuesday', 'h': 'Thursday'},
            'W': 'Wednesday', 'F': 'Friday',
            'S': {'a': 'Saturday', 'u': 'Sunday'}}

letter1 = input('please input the first character: ')
letter1 = letter1.upper()

if letter1 in ['T', 'S']:
    letter2 = input('please input the second character: ')
    print(weekList[letter1][letter2])
else:
    print(weekList[letter1])

```

### 3) 效果
```
please input the first character: t
please input the second character: u
Tuesday
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
