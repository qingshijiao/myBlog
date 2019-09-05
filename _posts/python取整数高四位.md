---
title: 【python实例54】取整数高四位

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
取一个整数a从右端开始的4〜7位
# 题解
## 1.
### 1) 程序分析
可以这样考虑：
(1)先使a右移4位。
(2)设置一个低4位全为1,其余全为0的数。可用~(~0<<4)
(3)将上面二者进行 & 运算。

**说明：** 一个字节是由 8 位二进制（0，1）组成，表示范围1111 1111- 0000 0000，通常将前四位成为高四位，后四位成为低四位。 然而题目中的整数没有限制范围，我们只需要取相应位数即可。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = int(input('input a number:\n'))
b = a >> 4
c = ~(~0 << 4)
d = b & c
# 八进制
print('%o\t%o' % (a, d))

```

### 3) 效果
```
input a number:
9
11	0
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
