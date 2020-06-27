---
title: 503. 下一个更大元素 II（Next Greater Element II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [503\. 下一个更大元素 II](https://leetcode-cn.com/problems/next-greater-element-ii/)

Difficulty: **中等**


给定一个循环数组（最后一个元素的下一个元素是数组的第一个元素），输出每个元素的下一个更大元素。数字 x 的下一个更大的元素是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 -1。

**示例 1:**

```
输入: [1,2,1]
输出: [2,-1,2]
解释: 第一个 1 的下一个更大的数是 2；
数字 2 找不到下一个更大的数； 
第二个 1 的下一个最大的数需要循环搜索，结果也是 2。
```

**注意:** 输入数组的长度不会超过 10000。


#### Solution

Language: **Java**

```java
​class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        int[] stack = new int[nums.length];
        int stackIndex = 0;
        //stack初始化
        for (int i = nums.length - 1; i >= 0; i--) {
            while (stackIndex > 0 && stack[stackIndex - 1] <= nums[i]) {
                //入栈前判断栈顶元素，若栈顶元素更小，则先出栈
                stackIndex--;
            }
            //入栈
            stack[stackIndex++] = nums[i];
        }
        //开始寻找更大的数
        for (int i = nums.length - 1; i >= 0; i--) {
            while (stackIndex > 0 && stack[stackIndex - 1] <= nums[i]) {
                //入栈前判断栈顶元素，若栈顶元素更小，则先出栈
                stackIndex--;
            }
            if (stackIndex == 0) {
                res[i] = -1;
            } else {
                res[i] = stack[stackIndex - 1];
            }
            //入栈
            stack[stackIndex++] = nums[i];
        }
        return res;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/next-greater-element-ii/)***
