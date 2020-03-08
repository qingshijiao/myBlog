---
title: 283.移动零 (Move Zeroes)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [283\. 移动零](https://leetcode-cn.com/problems/move-zeroes/)

Difficulty: **简单**


给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例:**

```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**说明**:

1.  必须在原数组上操作，不能拷贝额外的数组。
2.  尽量减少操作次数。

#### Solution1 - 双指针

Language: **Java**

```java
class Solution {
    public void moveZeroes(int[] nums) {
        for (int i = 0, j = 0; j < nums.length; j++) {
            if (nums[j] != 0) {
                int tmp = nums[j];
                nums[j] = nums[i];
                nums[i++] = tmp;
            }
        }
    }
}

```

#### Solution2 - 滚雪球

Language: **Java**

```java
​private void snowBallSolution(int[] nums) {
    int ballSize = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == 0) {
            ballSize++;
        } else if (ballSize > 0) {
            nums[i - ballSize] = nums[i];
            nums[i] = 0;
        }
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/move-zeroes/)
[wang-zi-hao-zain](https://leetcode-cn.com/problems/move-zeroes/solution/yi-dong-ling-javajian-ji-ti-jie-bao-li-shuang-zhi-/)***
