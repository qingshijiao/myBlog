---
title: 【第0011题】敏感词

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0011 题:** 敏感词文本文件 filtered_words.txt，里面的内容为以下内容，当用户输入敏感词语时，则打印出 Freedom，否则打印出 Human Rights。
```
北京
程序员
公务员
领导
牛比
牛逼
你娘
你妈
love
sex
jiangge
```

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-


def filtered_words(path='..\\text\\filtered_words.txt'):
    words = []
    with open(path, 'r', encoding='utf-8', newline='') as f:
        for line in f:
            words.append(line.strip())
    return words


def filtering():
    words = filtered_words()
    print(words)
    while True:
        # 注意 python3中input相当于python2中raw_input
        text = input('content: ').strip()
        if text in words:
            print('Freedom')
        else:
            print('Human Rights')


if __name__ == '__main__':
    filtering()

```

### 2) 效果

```
['北京', '程序员', '公务员', '领导', '牛比', '牛逼', '你娘', '你妈', 'love', 'sex', 'jiangge']
content: 程序员
Freedom
content: 程序
Human Rights
content:
```


---
***参考：
[wanlifeipeng](https://www.cnblogs.com/hupeng1234/p/6681466.html)***
