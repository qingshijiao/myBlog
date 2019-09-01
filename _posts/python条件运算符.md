---
title: 【python实例15】条件运算符

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
利用条件运算符的嵌套来完成此题：学习成绩>=90分的同学用A表示，60-89分之间的用B表示，60分以下的用C表示。

# 题解
## 1.
### 1) 程序分析

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


score = int(input('enter a score: \n'))
if score >= 90:
    grade = 'A'
elif score >= 60:
    grade = 'B'
else:
    grade = 'C'


print('%d belongs to %s' % (score, grade))

```

### 3) 效果
```
enter a score:
70
70 belongs to B
```

## 2.
### 1) 程序分析
程序分析：(a>b)?a:b这是条件运算符的基本例子。python 中没有三目运算符，有替代方法 h = "变量1" if a>b else "变量2"　

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


score = int(input('enter a score: \n'))
grade = 'A' if score >= 90 else ('B' if score >= 60 else 'C')

print('%d belongs to %s' % (score, grade))

```

### 3) 效果
```
enter a score:
70
70 belongs to B
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
