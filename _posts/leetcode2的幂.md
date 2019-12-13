---
title: 231.2的幂（Power of Two）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [231\. 2的幂](https://leetcode-cn.com/problems/power-of-two/)

Difficulty: **简单**


给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

**示例 1:**

```
输入: 1
输出: true
解释: 20 = 1
```

**示例 2:**

```
输入: 16
输出: true
解释: 24 = 16
```

**示例 3:**

```
输入: 218
输出: false
```


#### Solution

Language: **Java**

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/power-of-two/submissions/)
[jyd](https://leetcode-cn.com/problems/power-of-two/solution/power-of-two-er-jin-zhi-ji-jian-by-jyd/)***
