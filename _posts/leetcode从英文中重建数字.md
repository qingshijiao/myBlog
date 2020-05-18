---
title: 423. 从英文中重建数字 (Reconstruct Original Digits from English)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [423\. 从英文中重建数字](https://leetcode-cn.com/problems/reconstruct-original-digits-from-english/)

Difficulty: **中等**


给定一个**非空**字符串，其中包含字母顺序打乱的英文单词表示的数字`0-9`。按升序输出原始的数字。

**注意:**

1.  输入只包含小写英文字母。
2.  输入保证合法并可以转换为原始的数字，这意味着像 "abc" 或 "zerone" 的输入是不允许的。
3.  输入字符串的长度小于 50,000。

**示例 1:**

```
输入: "owoztneoer"

输出: "012" (zeroonetwo)
```

**示例 2:**

```
输入: "fviefuro"

输出: "45" (fourfive)
```


#### Solution

Language: **Java**

```java
​class Solution {
      public String originalDigits(String s) {
        int[] wordCnt = new int[26];
        for (char c : s.toCharArray()) {
            wordCnt[c - 'a']++;
        }

        int[] numCnt = new int[10];
        numCnt[0] = wordCnt['z' - 'a'];
        numCnt[2] = wordCnt['w' - 'a'];
        numCnt[4] = wordCnt['u' - 'a'];
        numCnt[6] = wordCnt['x' - 'a'];
        numCnt[8] = wordCnt['g' - 'a'];

        numCnt[1] = wordCnt['o' - 'a'] - numCnt[0] - numCnt[2] - numCnt[4];
        numCnt[3] = wordCnt['h' - 'a'] - numCnt[8];
        numCnt[5] = wordCnt['f' - 'a'] - numCnt[4];
        numCnt[7] = wordCnt['s' - 'a'] - numCnt[6];

        numCnt[9] = wordCnt['i' - 'a'] - numCnt[5] - numCnt[6] - numCnt[8];

        int len = 0;
        for (int c : numCnt) {
            len += c;
        }        
        char[] res = new char[len];
        
        len = 0;
        for (int i = 0; i <= 9; i++) {
            for (int j = 0; j < numCnt[i]; j++) {
                res[len++] = (char)('0' + i);
            }
        }

        return new String(res);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reconstruct-original-digits-from-english/submissions/)***
