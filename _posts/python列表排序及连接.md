---
title: 【python实例74】列表排序及连接

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
列表排序及连接。

# 题解
## 1.
### 1) 程序分析
排序可使用 sort() 方法，连接可以使用 + 号或 extend() 方法。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = [2, 3, 1]
b = [4, 5, 6]
a.sort()
print(a)

print(a + b)

a.extend(b)
print(a)

```

### 3) 效果
```
[1, 2, 3]
[1, 2, 3, 4, 5, 6]
[1, 2, 3, 4, 5, 6]
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
