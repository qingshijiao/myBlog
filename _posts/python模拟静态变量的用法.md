---
title: 【python实例41】模拟静态变量的用法

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
模仿静态变量的用法。
# 题解
## 1.
### 1) 程序分析
python 类的用法
### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-


def varfunc():
    var = 0
    print('var = %d' % var)
    var += 1


if __name__ == '__main__':
    for i in range(3):
        varfunc()


# 类的属性
# 作为类的一个属性
class Static:
    staticVar = 5

    def varfunc(self):
        self.staticVar += 1
        print(self.staticVar)


print(Static.staticVar)
a = Static()
for i in range(3):
    a.varfunc()


```

### 3) 效果
```
var = 0
var = 0
var = 0
5
6
7
8
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
