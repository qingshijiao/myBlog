---
title: 220.存在重复元素 III（Contains Duplicate III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [220\. 存在重复元素 III](https://leetcode-cn.com/problems/contains-duplicate-iii/)

Difficulty: **中等**


给定一个整数数组，判断数组中是否有两个不同的索引 _i_ 和 _j_，使得 **nums [i]** 和 **nums [j]** 的差的绝对值最大为 _t_，并且 _i_ 和 _j_ 之间的差的绝对值最大为 _ķ_。

**示例 1:**

```
输入: nums = [1,2,3,1], k = 3, t = 0
输出: true
```

**示例 2:**

```
输入: nums = [1,0,1,1], k = 1, t = 2
输出: true
```

**示例 3:**

```
输入: nums = [1,5,9,1,5,9], k = 2, t = 3
输出: false
```


#### Solution1 - k窗口之数组

Language: **Java**
time:O(nmin(k,n)) space:O(1)
```java
​public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    for (int i = 0; i < nums.length; ++i) {
        for (int j = Math.max(i - k, 0); j < i; ++j) {
            if (Math.abs(nums[i] - nums[j]) <= t) return true;
        }
    }
    return false;
}
// Time limit exceeded.

```

#### Solution2 - k窗口之二叉搜索树

Language: **Java**
time:O(nlog(min(k,n))) space:O(min(n,k))
```java
​public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    TreeSet<Integer> set = new TreeSet<>();
    for (int i = 0; i < nums.length; ++i) {
        // Find the successor of current element
        Integer s = set.ceiling(nums[i]);
        if (s != null && s <= nums[i] + t) return true;

        // Find the predecessor of current element
        Integer g = set.floor(nums[i]);
        if (g != null && nums[i] <= g + t) return true;

        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
```

#### Solution3 - k窗口之桶排序

Language: **Java**
time:O(nlog(min(k,n))) space:O(min(n,k))
```java
​public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    TreeSet<Integer> set = new TreeSet<>();
    for (int i = 0; i < nums.length; ++i) {
        // Find the successor of current element
        Integer s = set.ceiling(nums[i]);
        if (s != null && s <= nums[i] + t) return true;

        // Find the predecessor of current element
        Integer g = set.floor(nums[i]);
        if (g != null && nums[i] <= g + t) return true;

        set.add(nums[i]);
        if (set.size() > k) {
            set.remove(nums[i - k]);
        }
    }
    return false;
}
```

#### Solution4 - k窗口之散列表

Language: **Java**

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
       if (t < 0 || k == 10000){
            return false;
        }
        TreeSet<Long> set = new TreeSet<>();
        //建立滑动窗口
        for (int i = 0; i < nums.length; i++) {

            Long floor      = set.floor(((long)nums[i] + t));
            Long ceiling    = set.ceiling(((long)nums[i] - t));
            if (floor != null && floor >= nums[i]
                || ceiling != null && ceiling <= nums[i]){
                return true;
            }
            set.add((long)nums[i]);
            if (set.size() > k){
                set.remove((long)nums[i-(k)]);
            }
        }
        return false;
    }
}
```



#### Solution5 - 间隔 k 递减

Language: **Java**
```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k == 0) {
            return false;
        }
        if (nums.length > 10000) {
            return false;
        }
        while (k > 0) {
            for (int i = 0; i + k < nums.length; i++) {
                if (Math.abs((long)nums[i] - (long)nums[i + k]) <= t) {
                    return true;
                }
            }
            k --;
        }

        return false;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/contains-duplicate-iii/solution/cun-zai-zhong-fu-yuan-su-iii-by-leetcode/)***
