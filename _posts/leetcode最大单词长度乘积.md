---
title: 318.最大单词长度乘积 (Maximum Product of Word Lengths)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [318\. 最大单词长度乘积](https://leetcode-cn.com/problems/maximum-product-of-word-lengths/)

Difficulty: **中等**


给定一个字符串数组 `words`，找到 `length(word[i]) * length(word[j])` 的最大值，并且这两个单词不含有公共字母。你可以认为每个单词只包含小写字母。如果不存在这样的两个单词，返回 0。

**示例 1:**

```
输入: ["abcw","baz","foo","bar","xtfn","abcdef"]
输出: 16
解释: 这两个单词为 "abcw", "xtfn"。
```

**示例 2:**

```
输入: ["a","ab","abc","d","cd","bcd","abcd"]
输出: 4
解释: 这两个单词为 "ab", "cd"。
```

**示例 3:**

```
输入: ["a","aa","aaa","aaaa"]
输出: 0
解释: 不存在这样的两个单词。
```


#### Solution - 位运算

Language: **Java**

```java
​class Solution {
    public int maxProduct(String[] words) {
        int n = words.length;
        int[] wordsBit = new int[n];
        for (int i = 0; i < n; i++) {
            wordsBit[i] = convertWordToBit(words[i]);
        }
        int max = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if ((wordsBit[i] & wordsBit[j]) == 0) {
                    int newLength = words[i].length() * words[j].length();
                    max = max < newLength ? newLength : max;
                }
            }
        }
        return max;
    }

    private int convertWordToBit(String word) {
        int wordBit = 0;
        int n = word.length();
        for (int i = 0; i < n; i++) {
            wordBit = wordBit | (1 << (word.charAt(i) - 'a'));
        }
        return wordBit;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/maximum-product-of-word-lengths/solution/zui-da-dan-ci-chang-du-cheng-ji-by-leetcode/)***
