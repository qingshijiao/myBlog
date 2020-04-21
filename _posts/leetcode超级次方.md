---
title: 372.超级次方 (Super Pow)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [372\. 超级次方](https://leetcode-cn.com/problems/super-pow/)

Difficulty: **中等**


你的任务是计算 _a_<sup>_b_</sup> 对 1337 取模，_a_ 是一个正整数，_b_ 是一个非常大的正整数且会以数组形式给出。

**示例 1:**

```
输入: a = 2, b = [3]
输出: 8
```

**示例 2:**

```
输入: a = 2, b = [1,0]
输出: 1024
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int superPow(int a, int[] b) {
int c = 1337;
        int exp = 0;
        int phi = euler(c);
        //phi = 1140
        //System.out.println(phi);

        for(int i=0;i<b.length;i++){
            exp = (exp*10+b[i])%phi;
        }

        return quickPow(a,exp,c);
    }

    public int quickPow(int a,int exp,int c){
        int ans = 1;
        a %= c;
        while(exp > 0){
            if((exp&1) == 1){
                ans = (ans*a) %c;
            }
            exp=exp>>1;
            a = (a*a)%c;
        }
        return ans;
    }

    public int euler(int n){
        int ans = n;
        for(int i=2;i*i<n;i++){
            if(n%i==0){
                ans = ans/n*(n-1);
                while(n%i==0){
                    n/=i;
                }
            }
        }
        if(n>1){
            ans = ans/n*(n-1);
        }
        return ans;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/super-pow/submissions/)***
