---
title: 387.字符串中的第一个唯一字符 (First Unique Character in a String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [387\. 字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)

Difficulty: **简单**


给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

**注意事项：**您可以假定该字符串只包含小写字母。


#### Solution

Language: **Java**

```java
​class Solution {
    public int firstUniqChar(String s) {
        int res =s.length();
        for(int i='a';i<='z';i++){
            int firstIndex = s.indexOf((char)i);
            if (firstIndex == -1) continue;
            int lastIndex = s.lastIndexOf((char)i);
            if(firstIndex==lastIndex){
                res = Math.min(firstIndex,res);
            }
        }
        return res==s.length()?-1:res;

    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)***
