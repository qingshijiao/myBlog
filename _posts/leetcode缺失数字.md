---
title: 268.缺失数字（Missing Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [268\. 缺失数字](https://leetcode-cn.com/problems/missing-number/)

Difficulty: **简单**


给定一个包含 `0, 1, 2, ..., n` 中 _n_ 个数的序列，找出 0 .. _n_ 中没有出现在序列中的那个数。

**示例 1:**

```
输入: [3,0,1]
输出: 2
```

**示例 2:**

```
输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

**说明:**
你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?


#### Solution1 - 排序

Language: **Java**

```java
​class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);

        // 判断 n 是否出现在末位
        if (nums[nums.length-1] != nums.length) {
            return nums.length;
        }
        // 判断 0 是否出现在首位
        else if (nums[0] != 0) {
            return 0;
        }

        // 此时缺失的数字一定在 (0, n) 中
        for (int i = 1; i < nums.length; i++) {
            int expectedNum = nums[i-1] + 1;
            if (nums[i] != expectedNum) {
                return expectedNum;
            }
        }

        // 未缺失任何数字（保证函数有返回值）
        return -1;
    }
}
```

#### Solution2 - 哈希表

Language: **Java**

```java
​class Solution {
    public int missingNumber(int[] nums) {
        Set<Integer> numSet = new HashSet<Integer>();
        for (int num : nums) numSet.add(num);

        int expectedNumCount = nums.length + 1;
        for (int number = 0; number < expectedNumCount; number++) {
            if (!numSet.contains(number)) {
                return number;
            }
        }
        return -1;
    }
}
```

#### Solution3 - 位运算

Language: **Java**

```java
​class Solution {
    public int missingNumber(int[] nums) {
        int missing = nums.length;
        for (int i = 0; i < nums.length; i++) {
            missing ^= i ^ nums[i];
        }
        return missing;
    }
}
```

#### Solution4 - 数学

Language: **Java**

```java
class Solution {
    public int missingNumber(int[] nums) {
        int expectedSum = nums.length*(nums.length + 1)/2;
        int actualSum = 0;
        for (int num : nums) actualSum += num;
        return expectedSum - actualSum;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/missing-number/solution/que-shi-shu-zi-by-leetcode/)***
