---
title: 336.回文对 (Palindrome Pairs)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [336\. 回文对](https://leetcode-cn.com/problems/palindrome-pairs/)

Difficulty: **困难**


给定一组**唯一**的单词， 找出所有**_不同 _**的索引对`(i, j)`，使得列表中的两个单词， `words[i] + words[j]` ，可拼接成回文串。

**示例 1:**

```
输入: ["abcd","dcba","lls","s","sssll"]
输出: [[0,1],[1,0],[3,2],[2,4]]
解释: 可拼接成的回文串为 ["dcbaabcd","abcddcba","slls","llssssll"]
```

**示例 2:**

```
输入: ["bat","tab","cat"]
输出: [[0,1],[1,0]]
解释: 可拼接成的回文串为 ["battab","tabbat"]
```


#### Solution

Language: **Java**

```java
class Solution {

    /**
     * 查找回文对.
     *
     * <p>注意：该方法更快.</p>
     *
     * <p>解题思路：<a href="https://leetcode.com/problems/palindrome-pairs/discuss/79212/50ms-java-beats-99.88-using-Trie"
     *      target="_blank">字典树（Trie）</a>.</p>
     *
     * @param words 单词数组
     * @return 回文对的集合.
     */
    public List<List<Integer>> palindromePairs(String[] words) {
        int len;
        if (words == null || (len = words.length) < 2) {
            return Collections.emptyList();
        }

        // 将单词存入到 HashMap 中.
        TrieNode root = new TrieNode();
        for (int i = 0; i < len; ++i) {
            this.insert(root, words[i].toCharArray(), i);
        }

        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < len; ++i) {
            this.search(root, words[i].toCharArray(), i, result);
        }
        return result;
    }

    /**
     * 向字典树的某个节点中插入元素.
     *
     * @param root 字典树节点.
     * @param w 单词的字符数组
     * @param index 插入的索引位置
     */
    private void insert(TrieNode root, char[] w, int index) {
        int len = w.length;
        for (int i = 0; i < len; ++i) {
            if (this.isPalindromeBetween(w, i, len - 1)) {
                root.indexs.add(index);
            }

            int id = w[i] - 'a';
            if (root.children[id] == null) {
                root.children[id] = new TrieNode();
            }
            root = root.children[id];
        }
        root.indexs.add(index);
        root.id = index;
    }

    /**
     * 判断某个单词给定的前后两个索引之间的字符串是否是回文字符串.
     *
     * @param words 单词字符数组
     * @param left 左指针索引
     * @param right 右指针索引
     * @return 布尔值
     */
    private boolean isPalindromeBetween(char[] words, int left, int right) {
        while (left < right) {
            if (words[left++] != words[right--]) {
                return false;
            }
        }
        return true;
    }

    private void search(TrieNode root, char[] w, int pos, List<List<Integer>> result) {
        int len = w.length;
        for (int i = len - 1; i >= 0; --i) {
            if (root.id >= 0 && root.id != pos && this.isPalindromeBetween(w, 0, i)) {
                result.add(Arrays.asList(root.id, pos));
            }

            int id = w[i] - 'a';
            if (root.children[id] == null) {
                return;
            } else {
                root = root.children[id];
            }
        }

        for (int num : root.indexs) {
            if (num != pos) {
                result.add(Arrays.asList(num, pos));
            }
        }
    }

    /**
     * 字典树节点类.
     *
     * @author blinkfox on 2020-03-08.
     */
    private static class TrieNode {

        /**
         * 该字典树节点的所有子节点.
         */
        private TrieNode[] children;

        /**
         * 所有索引的集合.
         */
        List<Integer> indexs;

        /**
         * ASCII 索引值作为 ID.
         */
        private int id;

        /**
         * 构造方法.
         */
        TrieNode() {
            this.id = -1;
            this.indexs = new ArrayList<>();
            this.children = new TrieNode[26];
        }
    }

}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/palindrome-pairs/submissions/)***
