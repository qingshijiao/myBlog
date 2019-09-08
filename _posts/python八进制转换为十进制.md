---
title: 【python实例82】八进制转换为十进制

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
八进制转换为十进制

# 题解
## 1.
### 1) 程序分析
反向
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = input('请输入一个八进制数：')
# 使用列表推导式来写
lost = sum([int(n[-i]) * 8 ** (i - 1) for i in range(1, len(n) + 1)])
print('转换十进制数为：%s' % lost)

```

### 3) 效果
```
请输入一个八进制数：011
转换十进制数为：9
```

## 2.
### 1) 程序分析
正向
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = 0
p = input('input a octal number:\n')
for i in range(len(p)):
    n = n * 8 + ord(p[i]) - ord('0')
print(n)

```

### 3) 效果
```
input a octal number:
122
82
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
