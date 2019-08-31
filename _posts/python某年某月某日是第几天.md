---
title: 【python实例4】某年某月某日是第几天

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输入某年某月某日，判断这一天是这一年的第几天？

# 题解
## 1.
### 1) 程序分析
以3月5日为例，应该先把前两个月的加起来，然后再加上5天即本年的第几天，特殊情况，闰年且输入月份大于2时需考虑多加一天：

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


year = int(input('year:\n'))
month = int(input('mouth:\n'))
day = int(input('day:\n'))

months = (0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334)
if 0 < month <= 12:
    sum = months[month - 1]
else:
    print('data error')
sum += day
leap = 0
if (year % 400 == 0) or ((year % 4 == 0) and (year % 100 != 0)):
    leap = 1
if (leap == 1) and (month > 2):
    sum += 1
print('it is the %dth day.' % sum)

```
**说明：** print格式

### 3) 效果
```
year:
2019
mouth:
8
day:
31
it is the 243th day.
```
## 2.
### 1) 程序分析
将闰年和平年天数分别用两个元组存储

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


year = int(input("year：\n"))
month = int(input("month：\n"))
day = int(input("day：\n"))
months1 = [0, 31, 60, 91, 121, 152, 182, 213, 244, 274, 305, 335, 366]  # 闰年
months2 = [0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334, 365]  # 平年

if ((year % 4 == 0) and (year % 100 != 0)) or (year % 400 == 0):
    Dth = months1[month - 1] + day
else:
    Dth = months2[month - 1] + day
print("it is the %dth day" % Dth)

```

### 3) 效果
```
year：
2019
month：
8
day：
31
it is the 243th day
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
