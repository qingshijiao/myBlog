---
title: 461. 汉明距离（Hamming Distance）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [461\. 汉明距离](https://leetcode-cn.com/problems/hamming-distance/)

Difficulty: **简单**


两个整数之间的指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 `x` 和 `y`，计算它们之间的汉明距离。

**注意：**  
0 ≤ `x`, `y` < 2<sup>31</sup>.

**示例:**

```
输入: x = 1, y = 4

输出: 2

解释:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

上面的箭头指出了对应二进制位不同的位置。
```


#### Solution

Language: **Java**

```java
​class Solution {
  public int hammingDistance(int x, int y) {
    int xor = x ^ y;
    int distance = 0;
    while (xor != 0) {
      distance += 1;
      // remove the rightmost bit of '1'
      xor = xor & (xor - 1);
    }
    return distance;
  }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/hamming-distance/solution/yi-ming-ju-chi-by-leetcode/)***
