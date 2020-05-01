---
title: 390.消除游戏 (Elimination Game)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [390\. 消除游戏](https://leetcode-cn.com/problems/elimination-game/)

Difficulty: **中等**


给定一个从1 到 n 排序的整数列表。
首先，从左到右，从第一个数字开始，每隔一个数字进行删除，直到列表的末尾。
第二步，在剩下的数字中，从右到左，从倒数第一个数字开始，每隔一个数字进行删除，直到列表开头。
我们不断重复这两步，从左到右和从右到左交替进行，直到只剩下一个数字。
返回长度为 n 的列表中，最后剩下的数字。

**示例：**

```
输入:
n = 9,
1 2 3 4 5 6 7 8 9
2 4 6 8
2 6
6

输出:
6
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int lastRemaining(int n) {
        boolean left = true;
        int remaining = n;
        int step = 1;
        int res = 1;
        while (remaining > 1) {
            if (left || remaining % 2 == 1)
                res = res + step;
            remaining /= 2;
            step *= 2;
            left = !left;
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/elimination-game/)***
