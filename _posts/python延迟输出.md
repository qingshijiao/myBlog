---
title: 【python实例9】延迟输出

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
暂停一秒输出。

# 题解
## 1.
### 1) 程序分析
使用 time 模块的 sleep() 函数。

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

import time

myD = {1: 'a', 2: 'b'}
for key, vlaue in dict.items(myD):
    print(key, vlaue)
    # 暂停 1 秒
    time.sleep(1)

```

### 3) 效果
```
1 a
2 b
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
