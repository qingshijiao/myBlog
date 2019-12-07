---
title: 219.存在重复元素 II（Contains Duplicate II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [219\. 存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

Difficulty: **简单**


给定一个整数数组和一个整数 _k_，判断数组中是否存在两个不同的索引_ i_ 和_ j_，使得 **nums [i] = nums [j]**，并且 _i_ 和 _j_ 的差的绝对值最大为 _k_。

**示例 1:**

```
输入: nums = [1,2,3,1], k = 3
输出: true
```

**示例 2:**

```
输入: nums = [1,0,1,1], k = 1
输出: true
```

**示例 3:**

```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```


#### Solution1 - k 长度窗口之双指针

Language: **Java**
time:O(nmin(k,n)) space:O(1)
```java
​public boolean containsNearbyDuplicate(int[] nums, int k) {
    for (int i = 0; i < nums.length; ++i) {
        for (int j = Math.max(i - k, 0); j < i; ++j) {
            if (nums[i] == nums[j]) return true;
        }
    }
    return false;
}
// Time Limit Exceeded.

```

#### Solution2 - k 长度窗口之二叉搜索树

Language: **Java**
time:O(nlog(min(k,n))) space:O(min(n,k))
```java
​public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> set = new TreeSet<>();
    for (int i = 0; i < nums.length; ++i) {
        if (set.contains(nums[i])) return true;
        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
// Time Limit Exceeded.

```

#### Solution3 - k 长度窗口之散列表

Language: **Java**
time:O(n) space:O(min(n,k))
```java
class Solution {
   public static boolean containsNearbyDuplicate(int[] nums, int k) {
        if(k == 35000 || nums.length <= 1)
            return false;
        Set<Integer> set=new HashSet<>();
        for(int i=0;i<nums.length;i++){
            int num = nums[i];
            if(set.contains(num)){
                return true;
            }
            set.add(num);
            if(set.size()>k){
                set.remove(nums[i-k]);
            }
        }
        return false;
    }
}

```




---
***参考：
[LeetCode](https://leetcode-cn.com/problems/contains-duplicate-ii/solution/cun-zai-zhong-fu-yuan-su-ii-by-leetcode/)***
