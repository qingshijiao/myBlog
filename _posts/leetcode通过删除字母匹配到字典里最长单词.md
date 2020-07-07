---
title: 524. 通过删除字母匹配到字典里最长单词（Longest Word in Dictionary through Deleting）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [524\. 通过删除字母匹配到字典里最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)

Difficulty: **中等**


给定一个字符串和一个字符串字典，找到字典里面最长的字符串，该字符串可以通过删除给定字符串的某些字符来得到。如果答案不止一个，返回长度最长且字典顺序最小的字符串。如果答案不存在，则返回空字符串。

**示例 1:**

```
输入:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

输出: 
"apple"
```

**示例 2:**

```
输入:
s = "abpcplea", d = ["a","b","c"]

输出: 
"a"
```

**说明:**

1.  所有输入的字符串只包含小写字母。
2.  字典的大小不会超过 1000。
3.  所有输入的字符串长度不会超过 1000。


#### Solution

Language: **Java**

```java
​class Solution {
    public String findLongestWord(String s, List<String> d) {
        List<String> result = new ArrayList<>();
        d.forEach(str -> {
            int pos = 0;
            boolean flag = true; //是否把该字符添加进result;
            for(int i = 0;i < str.length();i++){ //遍历str，判断是否在s中可以通过删除其他字符出现
                if (pos == s.length()) {
                    flag = false;
                    break;
                }
                char c = str.charAt(i);
                pos = s.indexOf(c,pos) + 1;
                if(pos == 0)   {
                    flag = false;
                    break;
                }
            }
            if(flag)    result.add(str);
        });
        //对result进行排序
        Collections.sort(result,(s1,s2) -> {
            if(s1.length() == s2.length())    return s1.compareTo(s2);
            return s2.length() - s1.length();
        });
        //如果答案不存在，则返回空字符串
        if(result.size() == 0)   return "";
        else     return result.get(0);
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/solution/)***
