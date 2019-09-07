---
title: 【python实例75】条件输出

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
放松一下，算一道简单的题目。

# 题解
## 1.
### 1) 程序分析
输出口只有一个，要想 n == 3，必须要满足上面 4 个条件中的三个，观察知 i == 4 和 i ！= 4 对立.
i == 4 成立：i == 3 不成立，n 不为 3
i != 4 成立：i == 3 成立，i 为 3
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

for i in range(5):
    n = 0
    if i != 1: n += 1
    if i == 3: n += 1
    if i == 4: n += 1
    if i != 4: n += 1
    if n == 3: print(64 + i)

```

### 3) 效果
```
67
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
