---
title: 275.H指数 II（H-Index II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [275\. H指数 II](https://leetcode-cn.com/problems/h-index-ii/)

Difficulty: **中等**


给定一位研究者论文被引用次数的数组（被引用次数是非负整数），数组已经按照**升序排列**。编写一个方法，计算出研究者的 _h_ 指数。

h 指数的定义: “h 代表“高引用次数”（high citations），一名科研人员的 h 指数是指他（她）的 （N 篇论文中）**至多**有 h 篇论文分别被引用了**至少** h 次。（其余的 _N - h _篇论文每篇被引用次数**不多于** _h_ 次。）"

**示例:**

```
输入: citations = [0,1,3,5,6]
输出: 3
解释: 给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 0, 1, 3, 5, 6 次。
     由于研究者有 3 篇论文每篇至少被引用了 3 次，其余两篇论文每篇被引用不多于 3 次，所以她的 h 指数是 3。
```

**说明:**

如果 _h_ 有多有种可能的值 ，_h_ 指数是其中最大的那个。

**进阶：**

*   这是  的延伸题目，本题中的 `citations` 数组是保证有序的。
*   你可以优化你的算法到对数时间复杂度吗？


#### Solution1 - 二分法

Language: **Java**

```java
​public class Solution {

    // 思路：看 nums[mid] 和区间 [mid, len - 1] 的长度，即 len - 1 - mid + 1 = len - mid
    // 要返回的是 nums 中的值
    // [0, 1, 2, 5, 6]，
    // 以下的代码注释是 coder_hezi 帮助添加的，在此表示感谢

    public int hIndex(int[] citations) {
        int len = citations.length;
        // 特判
        if (len == 0 || citations[len - 1] == 0) {
            return 0;
        }
        int left = 0;
        int right = len - 1;
        while (left < right) {
            int mid = (left + right) >>> 1;
            // 比长度小，就得去掉该值
            if (citations[mid] < len - mid) {
                left = mid + 1;
            } else {
                // 比长度大是满足的，我们应该继续让 mid 往左走去尝试看有没有更小的 mid 值
                // 可以满足 mid 对应的值大于等于从 [mid, len - 1] 的长度
                right = mid;
            }
        }
        return len - left;
    }
}
```

#### Solution2 - 遍历

Language: **Java**

```java
class Solution {
    public int hIndex(int[] citations) {
        // 排序（注意这里是升序排序，因此下面需要倒序扫描）
        // 线性扫描找出最大的 i
        int i = 0;
        while (i < citations.length && citations[citations.length - 1 - i] > i) {
            i++;
        }
        return i;
    }


}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/h-index-ii/submissions/)
[liweiwei1419](https://leetcode-cn.com/problems/h-index-ii/solution/jian-er-zhi-zhi-er-fen-cha-zhao-by-liweiwei1419-2/)***
