---
title: 【python实例33】按逗号分隔列表

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
按逗号分隔列表。
# 题解
## 1.
### 1) 程序分析
join() 函数的用法
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

a = [1, 2, 3, 4, 5]
print(a)
b = ','.join(str(n) for n in a)
print(b)

```

### 3) 效果
```
[1, 2, 3, 4, 5]
1,2,3,4,5
```

## 2.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

l = [1, 2, 3, 4, 5, 6, 7]
# l = [1]
k = 1
for i in l:
    print(i, end=('' if k == len(l) else ','))
    k += 1

```

### 3) 效果
```
1,2,3,4,5,6,7
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
