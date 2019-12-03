---
title: 211.添加与搜索单词 - 数据结构设计（Add and Search Word - Data structure design）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [211\. 添加与搜索单词 - 数据结构设计](https://leetcode-cn.com/problems/add-and-search-word-data-structure-design/)

Difficulty: **中等**


设计一个支持以下两种操作的数据结构：

```
void addWord(word)
bool search(word)
```

search(word) 可以搜索文字或正则表达式字符串，字符串只包含字母 `.` 或 `a-z` 。 `.` 可以表示任何一个字母。

**示例:**

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**说明:**

你可以假设所有单词都是由小写字母 `a-z` 组成的。


#### Solution1 - 前缀树数组
Trie 树又称“前缀树”，它的典型应用对象是字符串，可以用于保存、统计。其特点是：用边表示字符，当走到叶子结点的时候，沿途所经过的边组成了一个字符串。其优点是：利用字符串的公共前缀来减少查询时间，最大限度地减少无谓的字符串比较，查询效率比哈希表高。

以下是根据题目示例："bad"、"dad"、"mad" 组件的 Trie 树，结点值为“1” 表示这是一个单词的结尾。
![](https://pic.leetcode-cn.com/12b1937712d90024f569004b7ad12ec6b2791548255e5418342bd4bb467221c2-image.png)

Language: **Java**

```java
​public class WordDictionary {

    class Node {
        private Node[] next;
        private boolean isWord;

        public Node() {
            next = new Node[26];
            isWord = false;
        }
    }

    private Node root;

    /**
     * Initialize your data structure here.
     */
    public WordDictionary3() {
        root = new Node();
    }

    /**
     * Adds a word into the data structure.
     */
    public void addWord(String word) {
        int len = word.length();
        Node curNode = root;
        for (int i = 0; i < len; i++) {
            char curChar = word.charAt(i);
            Node next = curNode.next[curChar - 'a'];
            if (next == null) {
                curNode.next[curChar - 'a'] = new Node();
            }
            curNode = curNode.next[curChar - 'a'];
        }
        if (!curNode.isWord) {
            curNode.isWord = true;
        }
    }

    /**
     * Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
     */
    public boolean search(String word) {
        return match(word, root, 0);
    }

    private boolean match(String word, Node node, int start) {
        if (start == word.length()) {
            return node.isWord;
        }
        char alpha = word.charAt(start);
        if (alpha == '.') {
            for (int i = 0; i < 26; i++) {
                if (node.next[i] != null && match(word, node.next[i], start + 1)) {
                    return true;
                }
            }
            return false;
        } else {
            if (node.next[alpha - 'a'] == null) {
                return false;

            }
            return match(word, node.next[alpha - 'a'], start + 1);
        }
    }
}

```

#### Solution2 - 前缀树哈希表

Language: **Java**

```java
​public class WordDictionary {

    class Node {
        private Node[] next;
        private boolean isWord;

        public Node() {
            next = new Node[26];
            isWord = false;
        }
    }

    private Node root;

    /**
     * Initialize your data structure here.
     */
    public WordDictionary3() {
        root = new Node();
    }

    /**
     * Adds a word into the data structure.
     */
    public void addWord(String word) {
        int len = word.length();
        Node curNode = root;
        for (int i = 0; i < len; i++) {
            char curChar = word.charAt(i);
            Node next = curNode.next[curChar - 'a'];
            if (next == null) {
                curNode.next[curChar - 'a'] = new Node();
            }
            curNode = curNode.next[curChar - 'a'];
        }
        if (!curNode.isWord) {
            curNode.isWord = true;
        }
    }

    /**
     * Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
     */
    public boolean search(String word) {
        return match(word, root, 0);
    }

    private boolean match(String word, Node node, int start) {
        if (start == word.length()) {
            return node.isWord;
        }
        char alpha = word.charAt(start);
        if (alpha == '.') {
            for (int i = 0; i < 26; i++) {
                if (node.next[i] != null && match(word, node.next[i], start + 1)) {
                    return true;
                }
            }
            return false;
        } else {
            if (node.next[alpha - 'a'] == null) {
                return false;

            }
            return match(word, node.next[alpha - 'a'], start + 1);
        }
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/add-and-search-word-data-structure-design/)
[liweiwei1419](https://leetcode-cn.com/problems/add-and-search-word-data-structure-design/solution/yu-dao-tong-pei-fu-shi-di-gui-chu-li-python-dai-ma/)***
