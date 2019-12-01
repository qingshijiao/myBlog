---
title: 208.实现 Trie (前缀树)（Implement Trie (Prefix Tree)）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [208\. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

Difficulty: **中等**


实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。

**示例:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");
trie.search("app");     // 返回 true
```

**说明:**

*   你可以假设所有的输入都是由小写字母 `a-z` 构成的。
*   保证所有输入均为非空字符串。


#### Solution

Language: **Java**

```java
class TrieNode{
    public TrieNode[] children = new TrieNode[26];
    public String item = "";
    public TrieNode(){

    }
}
class Trie{
	private TrieNode root;
    public Trie(){
        root = new TrieNode();
    }
     /** Inserts a word into the trie. */
	public void insert(String word){
		TrieNode node = root;
        int index = 0;
        while(index < word.length()){
            if(node.children[word.charAt(index) - 'a'] == null){
                node.children[word.charAt(index) - 'a'] = new TrieNode();
            }
            node = node.children[word.charAt(index) - 'a'];
            index ++;

        }
        node.item = word;
	}
    /** Returns if the word is in the trie. */
	public boolean search(String word){
		TrieNode node = root;
        int index = 0;
        while(index < word.length()){
            if(node.children[word.charAt(index) - 'a'] == null){
                return false;
            }
            node = node.children[word.charAt(index) - 'a'];
            index ++;

        }
        return node.item.equals(word);
	}
    /** Returns if the word is in the trie. */
	public boolean startsWith(String prefix){
		TrieNode node = root;
        int index = 0;
        while(index < prefix.length()){
            if(node.children[prefix.charAt(index) - 'a'] == null){
                return false;
            }
            node = node.children[prefix.charAt(index) - 'a'];
            index ++;

        }
        return true;
	}
}



/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/implement-trie-prefix-tree/submissions/)***
