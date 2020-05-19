---
title: 425. 单词方块 (Word Squares)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目
Given a set of words (without duplicates), find all word squares you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

For example, the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

b a l l
a r e a
l e a d
l a d y

**Note:**

There are at least 1 and at most 1000 words.
All words will have the exact same length.
Word length is at least 1 and at most 5.
Each word contains only lowercase English alphabet a-z.
 

Example 1:
```
Input:
["area","lead","wall","lady","ball"]

Output:
[
  [ "wall",
    "area",
    "lead",
    "lady"
  ],
  [ "ball",
    "area",
    "lead",
    "lady"
  ]
]

Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
 ```

Example 2:
```
Input:
["abat","baba","atan","atal"]

Output:
[
  [ "baba",
    "abat",
    "baba",
    "atan"
  ],
  [ "baba",
    "abat",
    "baba",
    "atal"
  ]
]

Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
```


#### Solution - 前缀树

Language: **Java**

```java
​class Solution {
public:
    struct TrieNode {
        vector<int> indexs;
        vector<TrieNode*> children;
        TrieNode(): children(26, nullptr) {}
    };
    TrieNode* buildTrie(vector<string>& words) {
        TrieNode *root = new TrieNode();
        for (int i = 0; i < words.size(); ++i) {
            TrieNode *t = root;
            for (int j = 0; j < words[i].size(); ++j) {
                if (!t->children[words[i][j] - 'a']) {
                    t->children[words[i][j] - 'a'] = new TrieNode();
                }
                t = t->children[words[i][j] - 'a'];
                t->indexs.push_back(i);
            }
        }
        return root;
    }
    vector<vector<string>> wordSquares(vector<string>& words) {
        TrieNode *root = buildTrie(words);
        vector<string> out(words[0].size());
        vector<vector<string>> res;
        for (string word : words) {
            out[0] = word;
            helper(words, 1, root, out, res);
        }
        return res;
    }
    void helper(vector<string>& words, int level, TrieNode* root, vector<string>& out, vector<vector<string>>& res) {
        if (level >= words[0].size()) {
            res.push_back(out);
            return;
        }
        string str = "";
        for (int i = 0; i < level; ++i) {
            str += out[i][level];
        }
        TrieNode *t = root;
        for (int i = 0; i < str.size(); ++i) {
            if (!t->children[str[i] - 'a']) return;
            t = t->children[str[i] - 'a'];
        }
        for (int idx : t->indexs) {
            out[level] = words[idx];
            helper(words, level + 1, root, out, res);
        }
    }
};

```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6006000.html)***
