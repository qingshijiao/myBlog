---
title: 293.翻转游戏(flip game)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip twoconsecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to compute all possible states of the string after one valid move.

For example, given s = "++++", after one move, it may become one of the following states:

[
  "--++",
  "+--+",
  "++--"
]
If there is no valid move, return an empty list [].

给一个只含有'+', '-'的字符串，每次可翻动两个连续的'+'，求有多少种翻法。

#### Solution

Language: **Java**

```java
public class Solution {
    public List<String> generatePossibleNextMoves(String s) {
        List<String> res = new ArrayList<>();
        char[] arr = s.toCharArray();
        for(int i = 1; i < s.length(); i++) {
            if(arr[i] == '+' && arr[i - 1] == '+') {
                arr[i] = '-';
                arr[i - 1] = '-';
                res.add(String.valueOf(arr));
                arr[i] = '+';
                arr[i - 1] = '+';
            }
        }

        return res;
    }
}

```


---
***参考：
[lightwindy](https://www.cnblogs.com/lightwindy/p/9666925.html)***
