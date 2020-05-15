---
title: 418. 屏幕可显示句子的数量

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目描述：
给你一个 rows x cols 的屏幕和一个用 非空 的单词列表组成的句子，请你计算出给定句子可以在屏幕上完整显示的次数。

**注意：**

一个单词不能拆分成两行。
单词在句子中的顺序必须保持不变。
在一行中 的两个连续单词必须用一个空格符分隔。
句子中的单词总量不会超过 100。
每个单词的长度大于0 且不会超过 10。
1 ≤ rows, cols ≤ 20,000.
示例：
示例 1：
```
输入：
rows = 2, cols = 8, 句子 sentence = ["hello", "world"]

输出：
1

解释：
hello---
world---

字符 '-' 表示屏幕上的一个空白位置。
```
示例 2：
```
输入：
rows = 3, cols = 6, 句子 sentence = ["a", "bcd", "e"]

输出：
2

解释：
a-bcd- 
e-a---
bcd-e-

字符 '-' 表示屏幕上的一个空白位置。
```
示例 3：
```
输入：
rows = 4, cols = 5, 句子 sentence = ["I", "had", "apple", "pie"]

输出：
1

解释：
I-had
apple
pie-I
had--

字符 '-' 表示屏幕上的一个空白位置。
```

#### Solution

Language: **python**

```python
class Solution:
    def wordsTyping(self, sentence: List[str], rows: int, cols: int) -> int:
        # 每个单词的长度
        ln = [len(s) for s in sentence]
        n = len(ln)
        all_len = sum(ln) + n # 所有单词长度(加上空格,最后单词也有)
        # 遍历 sentence 的位置
        idx = 0
        # 结果
        res = 0
        for i in range(rows):
            # 剩余的列
            remain_col = cols
            while remain_col > 0 :
                if ln[idx] <= remain_col:
                    remain_col -= ln[idx]
                    if remain_col > 0: remain_col -= 1
                    idx += 1
                    if idx == n:
                        # 从头开始,剩余的列的位置有放一个 sentence
                        div, mod = divmod(remain_col, all_len)
                        res += div + 1
                        remain_col = mod
                        idx = 0
                else:
                    break
        return res
```

---
***参考：
[九四干](https://zhuanlan.zhihu.com/p/107867796)***
