---
title: 260.只出现一次的数字 III（Single Number III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [260\. 只出现一次的数字 III](https://leetcode-cn.com/problems/single-number-iii/)

Difficulty: **中等**


给定一个整数数组 `nums`，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。

**示例 :**

```
输入: [1,2,1,3,2,5]
输出: [3,5]
```

**注意：**

1.  结果输出的顺序并不重要，对于上面的例子， `[5, 3]` 也是正确答案。
2.  你的算法应该具有线性时间复杂度。你能否仅使用常数空间复杂度来实现？


#### Solution - 异或

Language: **Java**

```java
​class Solution {
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for (int i : nums)// 一样的抵消,不一样的两个数字异或运算结果必定有一位是1
            xor ^= i;

        int mask = xor & (-xor);

        int[] ans = new int[2];
        for (int i : nums) {
            if ((i & mask) == 0)//== 0、 == mask 两种结果
                ans[0] ^= i;
            else
                ans[1] ^= i;
        }

        return ans;
    }
}
```

---
***参考：
[StackOverflow-](https://leetcode-cn.com/problems/single-number-iii/solution/java-yi-dong-yi-jie-xiao-lu-gao-by-spirit-9-9/)***
