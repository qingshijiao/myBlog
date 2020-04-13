---
title: 357.计算各个位数不同的数字个数 (Count Numbers with Unique Digits)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [357\. 计算各个位数不同的数字个数](https://leetcode-cn.com/problems/count-numbers-with-unique-digits/)

Difficulty: **中等**


给定一个**非负**整数 n，计算各位数字都不同的数字 x 的个数，其中 0 ≤ x < 10<sup>n </sup>。

**示例:**

```
输入: 2
输出: 91
解释: 答案应为除去 11,22,33,44,55,66,77,88,99 外，在 [0,100) 区间内的所有数字。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if(n==0)return 1;
        int[] dp=new int[n+1];
        dp[0]=1;
        dp[1]=10;
        for(int i=2;i<=n;i++){
            dp[i]=dp[i-1]+(dp[i-1]-dp[i-2])*(11-i);
        }
        if(n>=10)return dp[10];
        return dp[n];
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/count-numbers-with-unique-digits/submissions/)***
