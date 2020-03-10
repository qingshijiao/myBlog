---
title: 288.单词的唯一缩写 (Unique Word Abbreviation)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:
```
a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n

```
Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

Example:
```
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

#### Solution

Language: **Java**

```java
public class ValidWordAbbr {
    Map<String, Set<String>> map;
    public ValidWordAbbr(String[] dictionary) {
        map = new HashMap<>();
        for (String s : dictionary) {
            String abbr = getAbbr(s);
            if (!map.containsKey(abbr)) {
                map.put(abbr, new HashSet<String>());
            }
            map.get(abbr).add(s);
        }
    }

    public boolean isUnique(String word) {
        String abbr = getAbbr(word);
        if (!map.containsKey(abbr) || (map.get(abbr).contains(word) && map.get(abbr).size() == 1)) {
            return true;
        }
        return false;
    }

    private String getAbbr(String s) {
        if (s.length() < 3) {
            return s;
        }
        int len = s.length();
        return s.substring(0, 1) + (len - 2) + s.substring(len - 1);
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/unique-word-abbreviation/)
[轻风舞动](https://www.cnblogs.com/lightwindy/p/9602330.html)***
