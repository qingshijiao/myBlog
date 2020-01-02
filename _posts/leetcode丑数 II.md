---
title: 264.丑数 II（Ugly Number II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [264\. 丑数 II](https://leetcode-cn.com/problems/ugly-number-ii/)

Difficulty: **中等**


编写一个程序，找出第 `n` 个丑数。

丑数就是只包含质因数 `2, 3, 5` 的**正整数**。

**示例:**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明:** 

1.  `1` 是丑数。
2.  `n` **不超过**1690。


#### Solution1 - 动态规划

Language: **Java**

```java
​class Solution {
    private static int[] nums;
    public int nthUglyNumber(int n) {
        if (nums == null) {
            nums = new int[1690];
            int index2 = 0;
            int index3 = 0;
            int index5 = 0;

            int tmp = 1;
            nums[0] = 1;

            int value2 = 0;
            int value3 = 0;
            int value5 = 0;

            int cnt = 1;
            while (cnt < 1690) {
                value2 = nums[index2] * 2;
                value3 = nums[index3] * 3;
                value5 = nums[index5] * 5;
                tmp = Math.min(value2, Math.min(value3, value5));
                nums[cnt++] = tmp;
                if (tmp == value2) {
                    index2++;
                }
                if (tmp == value3) {
                    index3++;
                }
                if (tmp == value5) {
                    index5++;
                }
            }
        }
        return nums[n - 1];
    }
}
```

#### Solution2 - 最小堆

Language: **Java**

```java
​class Solution {
    public int nthUglyNumber(int n) {
        int[] ele = new int[]{2,3,5};
        PriorityQueue<Long> priorityQueue = new PriorityQueue<>();
        long[] res = new long[n];
        res[0] = 1;

        for (int i = 0; i < res.length; i++) {
            for (int j = 0; j < ele.length; j++) {
                // 用int存数据的时候，有些溢出的数据被堆排到了堆顶，用long可以避免溢出
                if (!priorityQueue.contains( (long)(res[i] * ele[j]) )) {
                    priorityQueue.add((long)(res[i] *ele[j]));
                }
            }
            if (i+1<res.length){
                res[i+1] = priorityQueue.poll();
            }
        }
//        System.out.println(Arrays.toString(res));
        return (int)res[n-1];
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/ugly-number-ii/submissions/)
[linzb-2](https://leetcode-cn.com/problems/ugly-number-ii/solution/zui-rong-yi-li-jie-de-si-lu-by-linzb-2/)***
