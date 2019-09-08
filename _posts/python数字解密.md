---
title: 【python实例89】数字解密

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
某个公司采用公用电话传递数据，数据是四位的整数，在传递过程中是加密的，加密规则如下：每位数字都加上5,然后用和除以10的余数代替该数字，再将第一位和第四位交换，第二位和第三位交换。

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


a = int(input('输入四个数字:\n'))
aa = [a // 1000, a % 1000 // 100,a % 100 // 10, a % 10]

for i in range(4):
    aa[i] += 5
    aa[i] %= 10
for i in range(2):
    aa[i], aa[3 - i] = aa[3 - i], aa[i]

print(aa)

```

### 3) 效果
```
输入四个数字:
1234
[9, 8, 7, 6]
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
