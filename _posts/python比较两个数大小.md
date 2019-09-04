---
title: 【python实例48】比较两个数大小

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
数字比较。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def compare(a, b):
    maxSum = max(a, b)
    minSum = min(a, b)
    print('%s比%s大' % (maxSum, minSum))


a = 10
b = 20
compare(a, b)


```

### 3) 效果
```
20比10大
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
