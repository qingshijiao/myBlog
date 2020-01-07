---
title: 274.H指数（H-Index）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [274\. H指数](https://leetcode-cn.com/problems/h-index/)

Difficulty: **中等**


给定一位研究者论文被引用次数的数组（被引用次数是非负整数）。编写一个方法，计算出研究者的 _h _指数。

h 指数的定义: “h 代表“高引用次数”（high citations），一名科研人员的 h 指数是指他（她）的 （N 篇论文中）**至多**有 h 篇论文分别被引用了**至少** h 次。（其余的 _N - h _篇论文每篇被引用次数**不多于** _h_ 次。）”

**示例:**

```
输入: citations = [3,0,6,1,5]
输出: 3
解释: 给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 3, 0, 6, 1, 5 次。
     由于研究者有 3 篇论文每篇至少被引用了 3 次，其余两篇论文每篇被引用不多于 3 次，所以她的 h 指数是 3。
```

**说明:** 如果 _h_ 有多种可能的值，_h_ 指数是其中最大的那个。


#### Solution1 - 排序

![](https://pic.leetcode-cn.com/Figures/274_H_index.svg)

Language: **Java**

```java
​public class Solution {
    public int hIndex(int[] citations) {
        // 排序（注意这里是升序排序，因此下面需要倒序扫描）
        Arrays.sort(citations);
        // 线性扫描找出最大的 i
        int i = 0;
        while (i < citations.length && citations[citations.length - 1 - i] > i) {
            i++;
        }
        return i;
    }
}
```

#### Solution2 - 计数
![](https://pic.leetcode-cn.com/Figures/274_H_index_2.svg)
Language: **Java**

```java
​public class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        int[] papers = new int[n + 1];
        // 计数
        for (int c: citations)
            papers[Math.min(n, c)]++;
        // 找出最大的 k
        int k = n;
        for (int s = papers[n]; k > s; s += papers[k])
            k--;
        return k;
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/h-index/solution/hzhi-shu-by-leetcode/)***
