---
title: 【python实例18】计算通项公式的值

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求s=a+aa+aaa+aaaa+aa...a的值，其中a是一个数字。例如2+22+222+2222+22222(此时共有5个数相加)，几个数相加由键盘控制。

# 题解
## 1.
### 1) 程序分析
关键是计算出每一项的值。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = int(input('n = '))
a = int(input('a = '))
sum = 0
total = 0
for i in range(n):
    sum += 10 ** i
    print(sum)
    total += sum * a


print(total)

```

### 3) 效果
```
n = 4
a = 4
1
11
111
1111
4936
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
