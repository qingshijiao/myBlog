---
title: 【python实例68】列表滑动

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有 n 个整数，使其前面各数顺序向后移 m 个位置，最后 m 个数变成最前面的 m 个数
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

m = 3
a = [1, 2, 3, 4, 5, 6, 7]


def rot(a, n):
    l = len(a)
    n = l - n
    return a[n:l] + a[0:n]


b = rot(a, m)

print(a)
print(b)


```

### 3) 效果
```
[1, 2, 3, 4, 5, 6, 7]
[5, 6, 7, 1, 2, 3, 4]
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = [1, 2, 3, 4, 5]    # 测试列表
print(a)
m = 3                  # 设置向后移动 3 位
for i in range(m):
    a.insert(0, a.pop())
print(a)

```

### 3) 效果
```
[1, 2, 3, 4, 5]
[3, 4, 5, 1, 2]
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
