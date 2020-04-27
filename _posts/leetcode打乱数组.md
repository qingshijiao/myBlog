---
title: 384.打乱数组 (Shuffle an Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [384\. 打乱数组](https://leetcode-cn.com/problems/shuffle-an-array/)

Difficulty: **中等**


打乱一个没有重复元素的数组。

**示例:**

```
// 以数字集合 1, 2 和 3 初始化数组。
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// 打乱数组 [1,2,3] 并返回结果。任何 [1,2,3]的排列返回的概率应该相同。
solution.shuffle();

// 重设数组到它的初始状态[1,2,3]。
solution.reset();

// 随机返回数组[1,2,3]打乱后的结果。
solution.shuffle();
```


#### Solution

Language: **Java**

```java
​class Solution {

    private int[] nums;

    private int[] randomNums;

    public Solution(int[] nums) {
        this.nums = nums;
        this.randomNums = nums.clone();
    }

    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }

    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        int end = nums.length;
        while (end > 0) {
            int randomIdx = ThreadLocalRandom.current().nextInt(0, end);
            int switchIdx = --end;
            int tmp = randomNums[switchIdx];
            randomNums[switchIdx] = randomNums[randomIdx];
            randomNums[randomIdx] = tmp;
        }

        return randomNums;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/shuffle-an-array/submissions/)***
