---
title: 34.在排序数组中查找元素的第一个和最后一个位置(Find First and Last Position of Element in Sorted Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```
示例 2:
```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```


# 题解

## 官方题解
### 1.线性扫描
**思想**：对链表进行从前到后，从后向前遍历。
**算法：**：首先，我们对 nums 数组从左到右做线性遍历，当遇到 target 时中止。如果我们没有中止过，那么 target 不存在，我们可以返回“错误代码” [-1, -1] 。如果我们找到了有效的左端点坐标，我们可以坐第二遍线性扫描，但这次从右往左进行。这一次，第一个遇到的 target 将是最右边的一个（因为最左边的一个存在，所以一定会有一个最右边的 target）。我们接下来只需要返回这两个坐标。


```
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] targetRange = {-1, -1};

        // find the index of the leftmost appearance of `target`.
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                targetRange[0] = i;
                break;
            }
        }

        // if the last loop did not find any index, then there is no valid range
        // and we return [-1, -1].
        if (targetRange[0] == -1) {
            return targetRange;
        }

        // find the index of the rightmost appearance of `target` (by reverse
        // iteration). it is guaranteed to appear.
        for (int j = nums.length-1; j >= 0; j--) {
            if (nums[j] == target) {
                targetRange[1] = j;
                break;
            }
        }

        return targetRange;
    }
}
```


**复杂度分析：**
- 时间复杂度：O(n)，这个暴力解法检测了num 数组中每个元素恰好两次，所以总运行时间是线性的。
- 空间复杂度：O(1)，线性扫描方法使用了固定大小的数组和几个整数，所以它的空间大小为常数级别的。



### 2.二分查找
**思想：** 两次二分查找，第一次查找左边界，左边界找不到，就返回 {-1，-1}，第二次查找右边界。
细节
```
if (nums[mid] > target || (left && target == nums[mid])) {
    hi = mid;  //不必减 1
} else {
    lo = mid+1;
}
```

```
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] targetRange = {-1, -1};

        int leftIdx = extremeInsertionIndex(nums, target, true);

        // assert that `leftIdx` is within the array bounds and that `target`
        // is actually in `nums`.
        if (leftIdx == nums.length || nums[leftIdx] != target) {
            return targetRange;
        }

        targetRange[0] = leftIdx;
        targetRange[1] = extremeInsertionIndex(nums, target, false)-1;

        return targetRange;
    }

    private int extremeInsertionIndex(int[] nums, int target, boolean left) {
        int lo = 0;
        int hi = nums.length;

        while (lo < hi) {
            int mid = (lo + hi) / 2;
            if (nums[mid] > target || (left && target == nums[mid])) {
                hi = mid;
            } else {
                lo = mid+1;
            }
        }

        return lo;
    }
}
```

**复杂度分析：**
- 时间复杂度：O(log2(n))，由于二分查找每次将搜索区间大约划分为两等分，所以至多有 log2(n) 次迭代。二分查找的过程被调用了两次，所以总的时间复杂度是对数级别的。
- 空间复杂度：O(1)，所有工作都是原地进行的，所以总的内存空间是常数级别的。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/zai-pai-xu-shu-zu-zhong-cha-zhao-yuan-su-de-di-yi-/)***
