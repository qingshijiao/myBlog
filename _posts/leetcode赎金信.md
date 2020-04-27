---
title: 383.赎金信 (Ransom Note)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [383\. 赎金信](https://leetcode-cn.com/problems/ransom-note/)

Difficulty: **简单**


给定一个赎金信 (`ransom`) 字符串和一个杂志(`magazine`)字符串，判断第一个字符串 `ransom` 能不能由第二个字符串 `magazines` 里面的字符构成。如果可以构成，返回 `true` ；否则返回 `false`。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)

**注意：**

你可以假设两个字符串均只含有小写字母。

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```


#### Solution

Language: **Java**

```java
​class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) {
            return false;
        }
        // 预留26个元素, 保存26个小写字母的对应值
        int[] caps = new int[26];
        for (char c : ransomNote.toCharArray()) {
            int index = magazine.indexOf(c, caps[c - 'a']);
            if (index == -1) {
                return false;
            }
            // 97 - n, 即数组的索引0对应字符a.1对应b...
            caps[c - 97] = index + 1;
        }
        return true;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/ransom-note/submissions/)***
