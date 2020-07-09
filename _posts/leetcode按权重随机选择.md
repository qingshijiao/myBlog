---
title: 528. 按权重随机选择 (Random Pick with Weight)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [528\. 按权重随机选择](https://leetcode-cn.com/problems/random-pick-with-weight/)

Difficulty: **中等**


给定一个正整数数组 `w` ，其中 `w[i]` 代表位置 `i` 的权重，请写一个函数 `pickIndex` ，它可以随机地获取位置 `i`，选取位置 `i` 的概率与 `w[i]` 成正比。

例如，给定一个值 [1，9] 的输入列表，当我们从中选择一个数字时，很有可能 10 次中有 9 次应该选择数字 9 作为答案。

**示例 1：**

```
输入：
["Solution","pickIndex"]
[[[1]],[]]
输出：[null,0]
```

**示例 2：**

```
输入：
["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
输出：[null,0,1,1,1,0]
```

**输入语法说明：**

输入是两个列表：调用成员函数名和调用的参数。`Solution` 的构造函数有一个参数，即数组 `w`。`pickIndex` 没有参数。输入参数是一个列表，即使参数为空，也会输入一个 [] 空列表。

**提示：**

*   `1 <= w.length <= 10000`
*   `1 <= w[i] <= 10^5`
*   `pickIndex` 将被调用不超过 `10000` 次


#### Solution

Language: **Java**

```java
​class Solution {
    
    int[] sum;
    int len;
    Random rand;

    public Solution(int[] w) {
        if(w == null) return;
        if(w.length < 1) return;
        
        this.len = w.length;
        this.sum = new int[len];
        
        sum[0] = w[0];
        for(int i = 1; i < len; i++){
            sum[i] = w[i] + sum[i-1];
        }
        
        this.rand = new Random();
    }
    
    public int pickIndex() {
        int point = this.rand.nextInt(sum[len - 1]) + 1;
        int pos = Arrays.binarySearch(this.sum, point);
        return pos >= 0 ? pos : -pos - 1;
            
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/random-pick-with-weight/)***
