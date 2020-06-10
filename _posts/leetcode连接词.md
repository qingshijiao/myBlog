---
title: 472.连接词 (Concatenated Words)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [472\. 连接词](https://leetcode-cn.com/problems/concatenated-words/)

Difficulty: **困难**


给定一个**不含重复**单词的列表，编写一个程序，返回给定单词列表中所有的连接词。

连接词的定义为：一个字符串完全是由至少两个给定数组中的单词组成的。

**示例:**

```
输入: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]

输出: ["catsdogcats","dogcatsdog","ratcatdogcat"]

解释: "catsdogcats"由"cats", "dog" 和 "cats"组成; 
     "dogcatsdog"由"dog", "cats"和"dog"组成; 
     "ratcatdogcat"由"rat", "cat", "dog"和"cat"组成。
```

**说明:**

1.  给定数组的元素总数不超过 `10000`。
2.  给定数组中元素的长度总和不超过 `600000`。
3.  所有输入字符串只包含小写字母。
4.  不需要考虑答案输出的顺序。


#### Solution

Language: **Java**

```java
​class Solution {
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
       List<String> res = new ArrayList<>();
        Set<String> set = new HashSet<>();
        int min = Integer.MAX_VALUE;
        for (String word : words) {
            if(word.length() == 0) continue;
            set.add(word);
            min = Math.min(min,word.length());
        }

        for (String word : words) {
            if (canbreak(word, set, 0, min)) {
                res.add(word);
            }
        }
        return res;
    }
    private boolean canbreak(String word, Set<String> set, int start, int min){
        for(int i = start+min; i <= word.length()-min; i++){
            if(set.contains(word.substring(start,i)) &&(set.contains(word.substring(i)) || canbreak(word,set,i,min))){
                return true;
            }
        }
        return false;
    }
}
```

---
***参考: 
[leetcode](https://leetcode-cn.com/problems/concatenated-words/submissions/)***
