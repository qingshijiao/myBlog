---
title: 386.字典序排数 (Lexicographical Numbers)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [386\. 字典序排数](https://leetcode-cn.com/problems/lexicographical-numbers/)

Difficulty: **中等**


给定一个整数 _n_, 返回从 _1 _到 _n _的字典顺序。

例如，

给定 _n_ =1 3，返回 [1,10,11,12,13,2,3,4,5,6,7,8,9] 。

请尽可能的优化算法的时间复杂度和空间复杂度。 输入的数据 _n _小于等于 5,000,000。


#### Solution

Language: **Java**

```java
​class Solution {
    int n;
    public List<Integer> lexicalOrder(int n) {
        this.n = n;
        int len = 0;
        int a = n;
        while(a!= 0){
            a/=10;
            len++;
        }
        List<Integer> ans = new ArrayList(n);
        for(int i = 1; i<10; i++){
            if(i>n) return ans;
            ans.add(i);
            lexicalOrder(len-1, ans, i);
        }
        return ans;

    }
    public void lexicalOrder(int len, List<Integer> ans, int porNum){
        if(len == 0) return;
        for(int i = 0; i<10; i++){
            int num = porNum*10+i;
            if(num>n) return;
            ans.add(num);
            lexicalOrder(len-1, ans, num);
        }
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/lexicographical-numbers/submissions/)***
