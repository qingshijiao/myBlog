---
title: 【python实例29】整数反转

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
给一个不多于5位的正整数，要求：一、求它是几位数，二、逆序打印出各位数字。
# 题解
## 1.
### 1) 程序分析
学会分解出每一位数。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

x = int(input("请输入一个数:\n"))
a = x // 10000
b = x % 10000 // 1000
c = x % 1000 // 100
d = x % 100 // 10
e = x % 10

if a != 0:
    print('5 位数：', e, d, c, b, a)
elif b != 0:
    print('4 位数：', e, d, c, b)
elif c != 0:
    print('3 位数：', e, d, c)
elif d != 0:
    print('2 位数：', e, d)
else:
    print('1 位数：', e)

```

### 3) 效果
```
请输入一个数:
1234
4 位数： 4 3 2 1
```

## 2.
### 1) 程序分析
用循环分解出每一位数。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = int(input('enter a number: '))
t = 0
cout = 0
while n != 0:
    t = t * 10 + n % 10
    n = n // 10
    cout += 1

print('the reversed number is %d, it has %d digit(s)' % (t, cout))


```

### 3) 效果
```
enter a number: 1234
the reversed number is 4321, it has 4 digit(s)
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
