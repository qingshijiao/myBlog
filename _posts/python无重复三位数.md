---
title: 【python实例1】无重复三位数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有四个数字：1、2、3、4，能组成多少个互不相同且无重复数字的三位数？各是多少？

# 题解
## 1.
### 1) 程序分析
可填在百位、十位、个位的数字都是1、2、3、4。组成所有的排列后再去 掉不满足条件的排列。

### 2) 代码
> 官网给的是 print(i, j, k)
> 我改成了 print(i * 100 + j * 10 + k)， 这样更体现三位数
```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

for i in range(1, 5):
    for j in range(1, 5):
        for k in range(1, 5):
            if (i != j) and (i != j) and (j != k):
                print(i * 100 + j * 10 + k)
```
**说明：** range 取值范围是**左闭右开**
### 3) 效果
```
121
123
124
131
132
134
141
142
143
212
213
214
231
232
234
241
242
243
312
313
314
321
323
324
341
342
343
412
413
414
421
423
424
431
432
434
```

---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
