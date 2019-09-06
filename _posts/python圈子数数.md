---
title: 【python实例69】圈子数数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有n个人围成一圈，顺序排号。从第一个人开始报数（从1到3报数），凡报到3的人退出圈子，问最后留下的是原来第几号的那位。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

data = [i+1 for i in range(20)]
print(data)
i = 1
while len(data) > 1:
    if i % 3 == 0:
        data.pop(0)
    else:
        data.insert(len(data), data.pop(0))
    i += 1
print(data)

```

### 3) 效果
```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
[20]
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
