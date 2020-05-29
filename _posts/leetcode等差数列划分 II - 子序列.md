---
title: 446. 等差数列划分 II - 子序列 (Arithmetic Slices II - Subsequence)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [446\. 等差数列划分 II - 子序列](https://leetcode-cn.com/problems/arithmetic-slices-ii-subsequence/)

Difficulty: **困难**


如果一个数列至少有三个元素，并且任意两个相邻元素之差相同，则称该数列为等差数列。

例如，以下数列为等差数列:

```
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

以下数列不是等差数列。

```
1, 1, 2, 5, 7
```

数组 A 包含 N 个数，且索引从 0 开始。该数组**子序列**将划分为整数序列 (P<sub style="display: inline;">0</sub>, P<sub style="display: inline;">1</sub>, ..., P<sub style="display: inline;">k</sub>)，P 与 Q 是整数且满足 0 ≤ P<sub style="display: inline;">0</sub> < P<sub style="display: inline;">1</sub> < ... < P<sub style="display: inline;">k</sub> < N。

如果序列 A[P<sub style="display: inline;">0</sub>]，A[P<sub style="display: inline;">1</sub>]，...，A[P<sub style="display: inline;">k-1</sub>]，A[P<sub style="display: inline;">k</sub>] 是等差的，那么数组 A 的**子序列** (P0，P1，…，PK) 称为等差序列。值得注意的是，这意味着 k ≥ 2。

函数要返回数组 A 中所有等差子序列的个数。

输入包含 N 个整数。每个整数都在 -2<sup>31</sup> 和 2<sup>31</sup>-1 之间，另外 0 ≤ N ≤ 1000。保证输出小于 2<sup>31</sup>-1。

**示例：**

```
输入：[2, 4, 6, 8, 10]

输出：7

解释：
所有的等差子序列为：
[2,4,6]
[4,6,8]
[6,8,10]
[2,4,6,8]
[4,6,8,10]
[2,4,6,8,10]
[2,6,10]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int numberOfArithmeticSlices(int[] A) {
 HashMap<Long, LinkedList<Integer>> quickAccessTarget = new HashMap<>();
        for (int x = 0; x < A.length; ++x) {
            LinkedList<Integer> indices = quickAccessTarget.getOrDefault((long)A[x], new LinkedList<Integer>());
            indices.add(x);
            quickAccessTarget.put((long)A[x], indices);
        }
        int out = 0;
        int[][] dp = new int[A.length][A.length];
        for (int x = 2; x < dp.length; ++x) {
            for (int y = x - 1; y >= 0; --y) {
                LinkedList<Integer> indicesX = quickAccessTarget.get((long)A[x] - 2L * ((long)A[x] - (long)A[y]));
                if (indicesX != null) {
                    for (int index : indicesX) {
                        if (index < y) {
                            dp[x][y] += dp[y][index] + 1;
                        }
                    }
                    out += dp[x][y];
                }
            }
        }
        return out;
    }
}
```


---
***参考:[leetcode](https://leetcode-cn.com/problems/arithmetic-slices-ii-subsequence/submissions/)***
