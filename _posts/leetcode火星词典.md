---
title: 269.火星词典（Alien Dictionary）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

269.Alien Dictionary
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

Example 1:
```
Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
```
Example 2:
```
Input:
[
  "z",
  "x"
]

Output: "zx"
```
Example 3:
```
Input:
[
  "z",
  "x",
  "z"
]

Output: ""

Explanation: The order is invalid, so return "".
```

**Note:**

- You may assume all letters are in lowercase.
- You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
- If the order is invalid, return an empty string.
- There may be multiple valid order of letters, return any one of them is fine.


#### Solution

Language: **Java**

```java
public class Solution {
    public String alienOrder(String[] words) {   // Topological sorting - Kahn's Algorithm
        if(words == null || words.length == 0) {
            return "";
        }
        Map<Character, Set<Character>> graph = new HashMap<>();
        Set<Character> set = new HashSet<>();
        for (String word : words) {
            for (int i = 0; i < word.length(); i++) {
                set.add(word.charAt(i));
            }
        }

        int[] inDegree = new int[26];
        for (int k = 1; k < words.length; k++) {
            String preStr = words[k - 1];
            String curStr = words[k];
            for (int i = 0; i < Math.min(preStr.length(), curStr.length()); i++) {
                char preChar = preStr.charAt(i);
                char curChar = curStr.charAt(i);
                if (preChar != curChar) {
                    if (!graph.containsKey(preChar)) {
                        graph.put(preChar, new HashSet<Character>());
                    }
                    if (!graph.get(preChar).contains(curChar)) {
                        inDegree[curChar - 'a']++;
                    }
                    graph.get(preChar).add(curChar);
                    break;
                }
            }
        }
        Queue<Character> queue = new LinkedList<>();
        for (int i = 0; i < inDegree.length; i++) {
            if (inDegree[i] == 0) {
                char c = (char)('a' + i);
                if (set.contains(c)) {
                    queue.offer(c);
                }
            }
        }
        StringBuilder sb = new StringBuilder();
        while (!queue.isEmpty()) {
            char c = queue.poll();
            sb.append(c);
            if (graph.containsKey(c)) {
                for (char l : graph.get(c)) {
                    inDegree[l - 'a']--;
                    if (inDegree[l - 'a'] == 0) {
                        queue.offer(l);
                    }
                }
            }
        }
        return sb.length() != set.size() ? "" : sb.toString();
    }
}
```

---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5023584.html)***
