---
title: 【python实例21】猴子吃桃

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
猴子吃桃问题：猴子第一天摘下若干个桃子，当即吃了一半，还不瘾，又多吃了一个第二天早上又将剩下的桃子吃掉一半，又多吃了一个。以后每天早上都吃了前一天剩下的一半零一个。到第10天早上想再吃时，见只剩下一个桃子了。求第一天共摘了多少。

# 题解
## 1.
### 1) 程序分析
采取逆向思维的方法，从后往前推断。

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

x = 1
for day in range(9, 0, -1):
    x = (x + 1) * 2
print(x)

```

### 3) 效果
```
1534
```
## 2.
### 1) 程序分析
递归

### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


# x 表示天数
def fun(x):
    if x == 10:
        return 1
    else:
        return (fun(x + 1) + 1) * 2


print(fun(1))


```
### 3) 效果
```
1534
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
