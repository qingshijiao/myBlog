---
title: 【第0012题】敏感语句

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0012 题：** 敏感词文本文件 filtered_words.txt，里面的内容 和 0011题一样，当用户输入敏感词语，则用 星号 * 替换，例如当用户输入「北京是个好城市」，则变成「**是个好城市」。
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

        for word in words:
            if word in text:
                replace_str = '*' * len(word)
                text = text.replace(word, replace_str)
        print(text)


if __name__ == '__main__':
    filtering()

```

### 2) 效果

```
['北京', '程序员', '公务员', '领导', '牛比', '牛逼', '你娘', '你妈', 'love', 'sex', 'jiangge']
content: 北京是个好城市
**是个好城市
content:
```


---
***参考：
[wanlifeipeng](https://www.cnblogs.com/hupeng1234/p/6681491.html)***
