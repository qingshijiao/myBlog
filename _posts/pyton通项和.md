---
title: 【python实例24】通项和

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
有一分数序列：2/1，3/2，5/3，8/5，13/8，21/13...求出这个数列的前20项之和。
# 题解
## 1.
### 1) 程序分析
请抓住分子与分母的变化规律。
### 2) 代码

```
total = 0
a, b = 1, 2
for i in range(1, 21):
    total += b / a
    a, b = b, a + b

print(total)

```

### 3) 效果
```
32.66026079864164
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
