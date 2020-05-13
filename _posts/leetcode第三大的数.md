---
title: 414. 第三大的数 (Third Maximum Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [414\. 第三大的数](https://leetcode-cn.com/problems/third-maximum-number/)

Difficulty: **简单**


给定一个非空数组，返回此数组中第三大的数。如果不存在，则返回数组中最大的数。要求算法时间复杂度必须是O(n)。

**示例 1:**

```
输入: [3, 2, 1]

输出: 1

解释: 第三大的数是 1.
```

**示例 2:**

```
输入: [1, 2]

输出: 2

解释: 第三大的数不存在, 所以返回最大的数 2 .
```

**示例 3:**

```
输入: [2, 2, 3, 1]

输出: 1

解释: 注意，要求返回第三大的数，是指第三大且唯一出现的数。
存在两个值为2的数，它们都排第二。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int thirdMax(int[] nums) {
        long max1 = Long.MIN_VALUE, max2 = Long.MIN_VALUE, max3 = Long.MIN_VALUE;
        int count = 0;
        for(int x : nums){
            if(x > max1){
                max3 = max2;
                max2 = max1;
                max1 = x;
            }else if(x > max2 && x != max1){
                max3 = max2;
                max2 = x;
            }else if(x > max3 && x != max2 && x != max1){
                max3 = x;
            }
        }
        if(max3 == Long.MIN_VALUE) return (int)max1;
        return (int)max3;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/third-maximum-number/submissions/)***
