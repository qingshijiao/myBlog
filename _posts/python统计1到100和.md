---
title: 【python实例45】统计 1 到 100 之和

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
统计 1 到 100 之和。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

total = 0
for i in range(1, 101):
    total += i

print('The sum is %d' % total)
print('Use sum() function: %d' % sum(range(1, 101)))


```

### 3) 效果
```
The sum is 5050
Use sum() function: 5050
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
