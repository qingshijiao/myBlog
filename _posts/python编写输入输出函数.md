---
title: 【python实例71】编写输入输出函数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目
编写input()和output()函数输入，输出5个学生的数据记录。

# 题解
## 1.
### 1) 程序分析


### 2) 代码

```
# !/usr/bin/python3
# -*- coding: UTF-8 -*-

n = 3
student = []
# student
# num: string
# name: string
# score[4]: list
for i in range(n):
    student.append(['', '', []])


def input_stu(stu):
    for i in range(n):
        stu[i][0] = input('input student num: ')
        stu[i][1] = input('input student name: ')
        for j in range(3):
            stu[i][2].append(int(input('score: ')))


def output_stu(stu):
    for i in range(n):
        print('%-6s%-10s' % (stu[i][0], stu[i][1]), end='')
        for j in range(3):
            print('%-8d' % stu[i][2][j], end='')
        print()


if __name__ == '__main__':
    input_stu(student)
    print(student)
    output_stu(student)

```

### 3) 效果
```
input student num: 1
input student name: aaa
score: 1
score: 2
score: 3
input student num: 2
input student name: bbb
score: 4
score: 5
score: 6
input student num: 3
input student name: ccc
score: 7
score: 8
score: 9
[['1', 'aaa', [1, 2, 3]], ['2', 'bbb', [4, 5, 6]], ['3', 'ccc', [7, 8, 9]]]
1     aaa       1       2       3
2     bbb       4       5       6
3     ccc       7       8       9
```



---
***参考：
[菜鸟教程](https://www.runoob.com/python/python-100-examples.html)***
