---
title: 【python实例83】求0至7组成的奇数个数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
求0—7所能组成的奇数个数。

# 题解
## 1.
### 1) 程序分析
组成1位数是4个。

组成2位数是7 * 4个。

组成3位数是7 * 8 * 4个。

组成4位数是7 * 8 * 8 * 4个。
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

sum = 4
s = 4
for j in range(2, 9):
    print(sum)
    if j <= 2:
        s *= 7
    else:
        s *= 8
    sum += s
print('sum = %d' % sum)

```

### 3) 效果
```
4
32
256
2048
16384
131072
1048576
sum = 8388608
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
