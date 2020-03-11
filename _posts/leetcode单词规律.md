---
title: 290.单词规律(Game of Life)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [290\. 单词规律](https://leetcode-cn.com/problems/word-pattern/)

Difficulty: **简单**


给定一种规律 `pattern` 和一个字符串 `str` ，判断 `str` 是否遵循相同的规律。

这里的 **遵循 **指完全匹配，例如， `pattern` 里的每个字母和字符串 `str`中的每个非空单词之间存在着双向连接的对应规律。

**示例1:**

```
输入: pattern = "abba", str = "dog cat cat dog"
输出: true
```

**示例 2:**

```
输入:pattern = "abba", str = "dog cat cat fish"
输出: false
```

**示例 3:**

```
输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false
```

**示例 4:**

```
输入: pattern = "abba", str = "dog dog dog dog"
输出: false
```

**说明:**
你可以假设 `pattern` 只包含小写字母， `str` 包含了由单个空格分隔的小写字母。    


#### Solution - 记录第一次出现的位置

Language: **Java**

```java
​class Solution
{
    public boolean wordPattern(String pattern, String str)
    {
        String[] arr = str.split(" ");
        if (pattern.length() != arr.length) return false;
        int len = pattern.length();
        for (int i = 0; i < len; i++) {
            if(pattern.indexOf(pattern.charAt(i)) != indexOf(arr, arr[i])){
                return false;
            }
        }
        return true;
    };

    public static int indexOf(String[] arrays, String searchString) {
        int ans = -1;
        for(int i = 0; i < arrays.length; i++) {
            if (arrays[i].equals(searchString)) {
                ans = i;
                break;
            };
        };
        return ans;
}

}
```

#### Solution - map

Language: **Java**

```java
​import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] words = str.split(" ");
        if (pattern.length() != words.length) {
            return false;
        }
        Map map = new HashMap();
        for (Integer i = 0; i < words.length; i++) {
            if (map.put(pattern.charAt(i), i) != map.put(words[i], i)) {
                return false;
            }
        }
        return true;
    }
}
```
---
***参考：
[LeetCode](https://leetcode-cn.com/problems/game-of-life/)
[homesway](https://leetcode-cn.com/problems/word-pattern/solution/yong-mapde-du-shi-zha-zha-zhi-jie-yong-indexofshi-/)
[hgnulb](https://www.cnblogs.com/hgnulb/p/11019884.html)***
