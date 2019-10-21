---
title: 128.最长连续序列（Longest Consecutive Sequence）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

示例:
```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```


# 题解

## 官方题解
### 1.暴力
**思路：**
因为一个序列可能在 nums 数组的任意一个数字开始，我们可以枚举每个数字作为序列的第一个数字，搜索所有的可能性。

```
class Solution {
    private boolean arrayContains(int[] arr, int num) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == num) {
                return true;
            }
        }

        return false;
    }
    public int longestConsecutive(int[] nums) {
        int longestStreak = 0;

        for (int num : nums) {
            int currentNum = num;
            int currentStreak = 1;

            while (arrayContains(nums, currentNum + 1)) {
                currentNum += 1;
                currentStreak += 1;
            }

            longestStreak = Math.max(longestStreak, currentStreak);
        }

        return longestStreak;
    }
}
```
**复杂度分析：**
- 时间复杂度：时间复杂度：O(n^3)
- 空间复杂度：O(1)

### 2.排序
**思路：**
如果我们可以将数组中的数字升序迭代，找连续数字会变得十分容易。为了将数组变得有序，我们将数组进行排序。

![](https://pic.leetcode-cn.com/48009532da24bc193697651f29266dee2c09f9fb4d9404846525ca2d4ff33cd8-image.png)

```
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }

        Arrays.sort(nums);

        int longestStreak = 1;
        int currentStreak = 1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i-1]) {
                if (nums[i] == nums[i-1]+1) {
                    currentStreak += 1;
                }
                else {
                    longestStreak = Math.max(longestStreak, currentStreak);
                    currentStreak = 1;
                }
            }
        }

        return Math.max(longestStreak, currentStreak);
    }
}
```
**复杂度分析：**
- 时间复杂度：O(nlgn)
- 空间复杂度：O(1)（或者 O(n)）,以上算法的具体实现中，由于我们将数组就低排序，所以额外的空间复杂度是常数级别的。如果不允许修改输入数组，我们需要额外的线性长度的空间来保存中间结果和排好序的数组。


### 3.哈希表和线性空间的构造
**思路：**


```
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> num_set = new HashSet<Integer>();
        for (int num : nums) {
            num_set.add(num);
        }

        int longestStreak = 0;

        for (int num : num_set) {
            if (!num_set.contains(num-1)) {
                int currentNum = num;
                int currentStreak = 1;

                while (num_set.contains(currentNum+1)) {
                    currentNum += 1;
                    currentStreak += 1;
                }

                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }

        return longestStreak;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n)
- 空间复杂度：O(n),为了实现 O(1) 的查询，我们对哈希表分配线性空间，以保存 nums 数组中的 O(n) 个数字。除此以外，所需空间与暴力解法一致。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/longest-consecutive-sequence/solution/zui-chang-lian-xu-xu-lie-by-leetcode/)***
