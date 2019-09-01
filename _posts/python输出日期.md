---
title: 【python实例16】输出指定格式日期

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
输出指定格式的日期。

# 题解
## 1.
### 1) 程序分析
使用 datetime 模块。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import datetime

# 输出今天日期，格式为 dd/mm/yyy。更多选项可以查看 strftime() 方法
print(datetime.date.today().strftime('%d/%m/%Y'))

# 创建日期对象
firstday = datetime.date(1941, 1, 5)
print(firstday.strftime('%d/%m/%Y'))

# 日期算术运算
secondday = firstday + datetime.timedelta(days=1)
print(secondday.strftime('%d/%m/%Y'))

# 日期替换
threeday = firstday.replace(year=firstday.year + 1)

print(threeday.strftime('%d/%m/%Y'))

```

### 3) 效果
```
01/09/2019
05/01/1941
06/01/1941
05/01/1942
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
