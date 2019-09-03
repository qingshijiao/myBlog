---
title: 【python实例40】逆序输出数组

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
将一个数组逆序输出。
# 题解
## 1.
### 1) 程序分析
用第一个与最后一个交换。
- 也可以用 a[::-1]
- a.reverse()

### 2) 代码

```
a = [9, 6, 5, 4, 1]
N = len(a)
print(a)
for i in range(int(len(a) / 2)):
    a[i], a[N - i - 1] = a[N - i - 1], a[i]
print(a)

```

### 3) 效果
```
[9, 6, 5, 4, 1]
[1, 4, 5, 6, 9]
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
