---
title: 338.比特位计数 (Counting Bits)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [338\. 比特位计数](https://leetcode-cn.com/problems/counting-bits/)

Difficulty: **中等**


给定一个非负整数 **num**。对于 **0 ≤ i ≤ num** 范围中的每个数字 **i **，计算其二进制数中的 1 的数目并将它们作为数组返回。

**示例 1:**

```
输入: 2
输出: [0,1,1]
```

**示例 2:**

```
输入: 5
输出: [0,1,1,2,1,2]
```

**进阶:**

*   给出时间复杂度为**O(n*sizeof(integer))**的解答非常容易。但你可以在线性时间**O(n)**内用一趟扫描做到吗？
*   要求算法的空间复杂度为**O(n)**。
*   你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 **__builtin_popcount**）来执行此操作。


#### Solution

Language: **Java**

```java
​class Solution {
    int res[];
    int max;
    public int[] countBits(int num) {
        res=new int[num+1];
        max=num;
        res[0]=0;
        if (num==0)
            return res;
        res[1]=1;
        plus(res[1],1);
        return res;
    }
    void plus(int num,int sum){
        num<<=1;
        if (num<=max) {
            res[num] = sum;
            plus(num, sum);
        }
        num++;
        if (num<=max){
            res[num]=sum+1;
            plus(num, sum+1);
        }
    }
}
```

```java
class Solution {
        public int[] countBits(int num) {
             int[] dp=new int[num+1];
            int count=0;
            for(int i=0;i<=num;i++)
            {
                dp[i]=dp[i>>1]+(i&1);
            }
            return dp;
        }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/counting-bits/submissions/)***
