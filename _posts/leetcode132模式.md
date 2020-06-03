---
title: 456. 132模式 (132 Pattern)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [456\. 132模式](https://leetcode-cn.com/problems/132-pattern/)

Difficulty: **中等**


给定一个整数序列：a<sub style="display: inline;">1</sub>, a<sub style="display: inline;">2</sub>, ..., a<sub style="display: inline;">n</sub>，一个132模式的子序列 a<sub style="display: inline;">**i**</sub>, a<sub style="display: inline;">**j**</sub>, a<sub style="display: inline;">**k**</sub> 被定义为：当 **i** < **j** < **k** 时，a<sub style="display: inline;">**i**</sub> < a<sub style="display: inline;">**k**</sub> < a<sub style="display: inline;">**j**</sub>。设计一个算法，当给定有 n 个数字的序列时，验证这个序列中是否含有132模式的子序列。

**注意：**n 的值小于15000。

**示例1:**

```
输入: [1, 2, 3, 4]

输出: False

解释: 序列中不存在132模式的子序列。
```

**示例 2:**

```
输入: [3, 1, 4, 2]

输出: True

解释: 序列中有 1 个132模式的子序列： [1, 4, 2].
```

**示例 3:**

```
输入: [-1, 3, 2, 0]

输出: True

解释: 序列中有 3 个132模式的的子序列: [-1, 3, 2], [-1, 3, 0] 和 [-1, 2, 0].
```


#### Solution

Language: **Java**

```java
class Solution {
    public boolean find132pattern(int[] nums) {
        int n = nums.length;
        if(n < 3)
            return false;
        int last = Integer.MIN_VALUE; // 132中的2
        int[] stk = new int[n];int top = -1;// 用来存储132中的3
        for(int i=n-1; i>=0; i--){
            if(nums[i] < last) // 若出现132中的1则返回正确值
                return true;
            while(top>-1 && stk[top] < nums[i]){ //单调递减栈
                last = stk[top];
                top--;
            }
            //弹完之后，last更新为在以nums[i]为最大值的[i,~]区间内的次大值
            //若下一个nums[i]<last，则说明找到了132
            stk[++top] = nums[i];
        }
        return false;
    }
}
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/132-pattern/)***
