---
title: 422. 有效的单词方块（Valid Word Abbreviation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
给你一个单词序列，判断其是否形成了一个有效的单词方块。
有效的单词方块是指此由单词序列组成的文字方块的 
第 k 行 和 第 k 列 (0 ≤ k < max(行数, 列数)) 
所显示的字符串完全相同。
示例：

输入：
```
[
 "abcd",
 "bnrt",
 "crmy",
 "dtye"
]
1
2
3
4
5
6
输出：true
解释：

第 1 行和第 1 列都是 "abcd"。
第 2 行和第 2 列都是 "bnrt"。
第 3 行和第 3 列都是 "crmy"。
第 4 行和第 4 列都是 "dtye"。
因此，这是一个有效的单词方块。
```

```
输入：

[
 "ball",
 "area",
 "read",
 "lady"
]
1
2
3
4
5
6
输出：false
解释：

第 3 行是 "read" ，然而第 3 列是 "lead"。
因此，这 不是 一个有效的单词方块。
```

**注意：**
- 给定的单词数大于等于 1 且不超过 500。
- 单词长度大于等于 1 且不超过 500。
- 每个单词只包含小写英文字母 a-z。

#### Solution

Language: **Java**

```java
public class Solution {
    public boolean validWordSquare(List<String> words) {
        for (int i = 0; i < words.size(); i++) {
            String word = words.get(i);
            for (int j = 0; j < word.length(); j++) {
                if (words.size() < j+1 || words.get(j).length() < i+1 || word.charAt(j) != words.get(j).charAt(i)){
                    return false;
                }
            }
        }
        return true;
    }
}
```
---
***参考：
[jianshu](https://www.jianshu.com/p/374023590efb)***
