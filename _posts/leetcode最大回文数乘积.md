---
title: 479. 最大回文数乘积 (Largest Palindrome Product)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [479\. 最大回文数乘积](https://leetcode-cn.com/problems/largest-palindrome-product/)

Difficulty: **困难**


你需要找到由两个 n 位数的乘积组成的最大回文数。

由于结果会很大，你只需返回最大回文数 mod 1337得到的结果。

**示例:**

输入: 2

输出: 987

解释: 99 x 91 = 9009, 9009 % 1337 = 987

**说明:**

n 的取值范围为 [1,8]。


#### Solution

Language: **Java**

```java
​class Solution {
    public int largestPalindrome(int n) {
        if(n == 1) return 9;
        //计算给定位数的最大值
        long max = (long)Math.pow(10,n) - 1;
        //从max - 1开始循环，原因见上文
        for(long i = max - 1; i > max / 10; i--){
            //1. 构造回文数
            String s1 = String.valueOf(i);
            long rev = Long.parseLong(s1 + new StringBuilder(s1).reverse().toString());
            //2. 检验该回文数能否由给定的数相乘得到
            for(long x = max; x * x >= rev; x --){
                if(rev % x == 0) return (int)(rev % 1337);
            }
        }
        return -1;
    }
}
```

```java
class Solution {
    public int largestPalindrome(int n) {
        int[] res = {9, 987, 123, 597, 677, 1218, 877, 475};
        return res[n-1];
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/largest-palindrome-product/)***
