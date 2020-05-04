---
title: 398.随机数索引 (Random Pick Index)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [398\. 随机数索引](https://leetcode-cn.com/problems/random-pick-index/)

Difficulty: **中等**


给定一个可能含有重复元素的整数数组，要求随机输出给定的数字的索引。 您可以假设给定的数字一定存在于数组中。

**注意：**
数组大小可能非常大。 使用太多额外空间的解决方案将不会通过测试。

**示例:**

```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) 应该返回索引 2,3 或者 4。每个索引的返回概率应该相等。
solution.pick(3);

// pick(1) 应该返回 0。因为只有nums[0]等于1。
solution.pick(1);
```


#### Solution

Language: **Java**

```java
​class Solution {

    int[] numArr;
    HashMap<Integer, Integer> hashMap = new HashMap<>();

    public Solution(int[] nums) {
        this.numArr = nums;
    }

    public int pick(int target) {
        int startIndex = hashMap.getOrDefault(target, 0);
        int findIndex = -1;
        for (int i = startIndex + 1; i < numArr.length; i++) {
            if (numArr[i] == target) {
                findIndex = i;
                break;
            }
        }
        if (findIndex < 0) {
            for (int i = 0; i <= startIndex; i++) {
                if (numArr[i] == target) {
                    findIndex = i;
                    break;
                }
            }
        }
        hashMap.put(target,findIndex);
        return findIndex;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/random-pick-index/submissions/)***
