---
title: 320.列举单词的全部缩写

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Write a function to generate the generalized abbreviations of a word.

Example:
```
Given word = "word", return the following list (order does not matter):
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```

#### Solution - 回溯法

Language: **Java**

```java
​public class Solution {
    public List<String> generateAbbreviations(String word) {
        List<String> result = new ArrayList<String>();
        StringBuilder sb = new StringBuilder();
        explore(0, sb, 0, result, word);
        return result;
    }
    public void explore(int cur, StringBuilder sb, int count, List<String> result, String word) {
        //到头了，返回条件
        if (cur == word.length()) {
            int i = sb.length();
            if (count != 0) {
                sb.append(count);
            }
            result.add(sb.toString());
            sb.delete(i, sb.length());
            return;
        }
        //abrv this char
        explore(cur + 1, sb, count + 1, result, word);

        //keep this char
        int i = sb.length();
        if (count != 0) {
            sb.append(count);
        }
        sb.append(word.charAt(cur));
        explore(cur + 1, sb, 0, result, word);
        sb.delete(i, sb.length());
    }
}
```

---
***参考:
[liuqi627](https://segmentfault.com/a/1190000005762481)***
