---
title: 【第0006题】日记中重要词

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0006 题：** 你有一个目录，放了你一个月的日记，都是 txt，为了避免分词的问题，假设内容都是英文，请统计出你认为每篇日记最重要的词。

# 题解
## 1.

### 1)代码
```
from collections import Counter
import re
import os


def get_word(txt_file):
    """
    从一个txt文件中找出出现次数最高的词及其对应次数，以元组形式返回
    """
    # 过滤词
    stop_word = ['the', 'in', 'of', 'and', 'to', 'has', 'that', 'this', 's', 'is', 'are', 'a', 'with', 'as', 'an']

    # 打开文件并且将内容转为小写
    f = open(txt_file, 'r')
    content = f.read().lower()
    # 根据正则式返回文章所有词
    pat = '[a-z0-9\']+'
    words = re.findall(pat, content)
    # 统计词的数量
    word_list = Counter(words)
    # 过滤词去掉
    for i in stop_word:
        word_list[i] = 0

    f.close()
    return word_list.most_common()[0]


def traverse_file(path):
    """
    遍历路径文件夹中的所有文件，并调用get_word函数，输出统计结果
    """
    for txt_name in os.listdir(path):
        # 根据路径 + 文件名打开文件
        txt_file = os.path.join(path, txt_name)
        # 调用get_word函数
        most_important = get_word(txt_file)
        print(most_important[0] + ' is the most important word in the essay:' + txt_name)

        print('the using times of ' + most_important[0] + " is:" + repr(most_important[1]))
        print('')


if __name__ == "__main__":
    path = 'E:\VirtualDesktop\code\pyCode\Test\\text'
    traverse_file(path)

```



---
***参考：
[chenjieping1995](https://blog.csdn.net/jacky_chenjp/article/details/52268272)***
