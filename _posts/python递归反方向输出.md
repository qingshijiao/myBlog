---
title: 【python实例27】递归反方向输出

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
利用递归函数调用方式，将所输入的5个字符，以相反顺序打印出来。
# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
def output(s, l):
    if l == 0:
        return
    print(s[l - 1], end='')
    output(s, l - 1)


s = input('Input a string: ')
output(s, len(s))

```

### 3) 效果
```
Input a string: abcdef
fedcba
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
