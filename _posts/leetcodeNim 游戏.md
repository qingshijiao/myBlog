---
title: 293.翻转游戏(flip game)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to compute all possible states of the string after one valid move.

For example, given s = "++++", after one move, it may become one of the following states:
```
[
  "--++",
  "+--+",
  "++--"
]
If there is no valid move, return an empty list [].
```

**解析：**

这道题让我们把相邻的两个++变成--，真不是一道难题，我们就从第二个字母开始遍历，每次判断当前字母是否为+，和之前那个字母是否为+，如果都为加，则将翻转后的字符串存入结果中即可


#### Solution

Language: **Java**

```java
public class Solution {
    public List<String> generatePossibleNextMoves(String s) {
        List<String> result = new ArrayList<String>();
        for (int i = 0; i < s.length() - 1; i++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                String flip = s.substring(0, i) + "--" + s.substring(i + 2);
                result.add(flip);
            }
        }
        return result;
    }
}

```

---
***参考：
[sam_justin](https://blog.csdn.net/samjustin1/article/details/52389147)***
