---
title: 【python实例20】球反弹

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
一球从100米高度自由落下，每次落地后反跳回原高度的一半；再落下，求它在第10次落地时，共经过多少米？第10次反弹多高？

# 题解
## 1.
### 1) 程序分析
### 2) 代码

```
hei = 100  # 总高度
tim = 10  # 次数
height = []  # 每次反弹高度
for i in range(2, tim + 1):  # 计算第二次落地到第十次落地
    hei /= 2
    height.append(hei)

print('第10次落地时，反弹%s高' % (min(height) / 2))  # 第十次反弹为第十次落地距离的一半
print('第10次落地时，经过%s米' % (sum(height) * 2 + 100))  # 总和加上第一次的 100

```

### 3) 效果
```
第10次落地时，反弹0.09765625高
第10次落地时，经过299.609375米
```


---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
