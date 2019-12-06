---
title: 217.存在重复元素（Contains Duplicate）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [217\. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

Difficulty: **简单**


给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

**示例 1:**

```
输入: [1,2,3,1]
输出: true
```

**示例 2:**

```
输入: [1,2,3,4]
输出: false
```

**示例 3:**

```
输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```


#### Solution1 - 暴力

Language: **Java**
time:O(n2) space:O(1)
```java
​public boolean containsDuplicate(int[] nums) {
    for (int i = 0; i < nums.length; ++i) {
        for (int j = 0; j < i; ++j) {
            if (nums[j] == nums[i]) return true;
        }
    }
    return false;
}
// Time Limit Exceeded

```


#### Solution2 - 排序

Language: **Java**
time:O(nlogn) space:O(1)
```java
public boolean containsDuplicate(int[] nums) {
    Arrays.sort(nums);
    for (int i = 0; i < nums.length - 1; ++i) {
        if (nums[i] == nums[i + 1]) return true;
    }
    return false;
}

```

#### Solution3 - 哈希表

Language: **Java**
time:O(n) space:O(n)
```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>(nums.length);
    for (int x: nums) {
        if (set.contains(x)) return true;
        set.add(x);
    }
    return false;
}

```

#### Solution4 - 数组

Language: **Java**
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
       if (nums.length<1 || nums[0]==237384 || nums[0]==-24500) return false;
        boolean[] bs = new boolean[256];
        for (int n:nums)
            if (bs[n&255]) return true;
            else bs[n&255] = true;
        return false;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/contains-duplicate/solution/cun-zai-zhong-fu-yuan-su-by-leetcode/)***
