---
title: 287.寻找重复数 (Find the Duplicate Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [287\. 寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)

Difficulty: **中等**


给定一个包含 _n_ + 1 个整数的数组 _nums_，其数字都在 1 到 _n _之间（包括 1 和 _n_），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

**示例 1:**

```
输入: [1,3,4,2,2]
输出: 2
```

**示例 2:**

```
输入: [3,1,3,4,2]
输出: 3
```

**说明：**

1.  **不能**更改原数组（假设数组是只读的）。
2.  只能使用额外的 _O_(1) 的空间。
3.  时间复杂度小于 _O_(_n_<sup>2</sup>) 。
4.  数组中只有一个重复的数字，但它可能不止重复出现一次。


#### Solution1 - 排序

Language: **Java**
time:O(nlgn) space:O(1)
```java
​class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i-1]) {
                return nums[i];
            }
        }

        return -1;
    }
}

```

#### Solution2 - 集合

Language: **Java**
time:O(n) space:O(n)
```java
class Solution {
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            }
            seen.add(num);
        }

        return -1;
    }
}

```


#### Solution3 - 弗洛伊德的乌龟和兔子（循环检测）

![](https://pic.leetcode-cn.com/Figures/287/Slide4.PNG)
![](https://pic.leetcode-cn.com/Figures/287/Slide12.PNG)
![](https://pic.leetcode-cn.com/Figures/287/Slide15.PNG)

Language: **Java**
time:O(n) space:O(1)
```java
class Solution {
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            }
            seen.add(num);
        }

        return -1;
    }
}

```

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0;
        int fast = 0;
        slow = nums[slow];
        fast = nums[nums[fast]];
        while(slow != fast){
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        int pre1 = 0;
        int pre2 = slow;
        while(pre1 != pre2){
            pre1 = nums[pre1];
            pre2 = nums[pre2];
        }
        return pre1;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/find-the-duplicate-number/solution/xun-zhao-zhong-fu-shu-by-leetcode/)***
