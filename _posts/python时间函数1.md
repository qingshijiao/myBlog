---
title: 【python实例92】时间函数2

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
时间函数举例2。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


import time

start = time.time()
# 延时作用
for i in range(3000):
    print(i)
end = time.time()

print(end - start)


```

### 3) 效果
```
...
2991
2992
2993
2994
2995
2996
2997
2998
2999
0.027925491333007812
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
