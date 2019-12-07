---
title: 【第0004题】统计单词出现次数

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目

**第 0004 题：** 任一个英文的纯文本文件，统计其中的单词出现的个数。

# 题解
## 1.

### 1)代码
```
import os

# 不加则默认当前目录
# os.chdir('C:/workspace')


def count_words(inputname):
    # 打开文件，默认当前目录
    fh = open(inputname)
    # 读文件内容
    read_fh = fh.read()
    # 单词个数
    number = 1
    # 单词
    is_alpha = []
    # 单词字典
    dict_words = {}

    for word in read_fh:
        # 判断是否为英文字母或者分隔符
        if word.isalpha():
            is_alpha.append(word)
        elif word == '\t' or word == '\n' or word == ' ':
            is_alpha.append(word)
    # 过滤掉非单词的文本
    fh_alpha = ''.join(is_alpha)
    # 将文本分隔为单词列表
    fh_words = fh_alpha.split()
    # 统计单词的数目
    for words in fh_words:
        words = words.lower()
        if words not in dict_words:
            dict_words[words] = number
        else:
            dict_words[words] = dict_words[words] + 1

    print(dict_words)


count_words("words.txt")

```



---
***参考：
[no_giveup](https://blog.csdn.net/no_giveup/article/details/51348314)***
