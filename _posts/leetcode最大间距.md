---
title: 164.最大间距（Maximum Gap）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个无序的数组，找出数组在排序之后，相邻元素之间最大的差值。

如果数组元素个数小于 2，则返回 0。

示例 1:
```
输入: [3,6,9,1]
输出: 3
解释: 排序后的数组是 [1,3,6,9], 其中相邻元素 (3,6) 和 (6,9) 之间都存在最大差值 3。
```
示例 2:
```
输入: [10]
输出: 0
解释: 数组元素个数小于 2，因此返回 0。
```

**说明:**

你可以假设数组中所有元素都是非负整数，且数值在 32 位有符号整数范围内。
请尝试在线性时间复杂度和空间复杂度的条件下解决此问题。


# 题解

## 官方题解
### 1.比较排序
**思路：**
```
class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        Arrays.sort(nums);

        int maxGap = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            maxGap = Math.max(nums[i + 1] - nums[i], maxGap);
        }
        return maxGap;

    }
}
```
**复杂度分析：**
- 时间复杂度：O(nlogn)。排序的复杂度是 O(nlogn)，遍历的复杂度是 O(n)，总复杂度是 O(nlogn)。
- 空间复杂度：除去输入数组之外，不需要额外空间（因为大多数都是原地排序）。


### 2.基数排序
**思路：**
```
int maximumGap(vector<int>& nums)
{
    if (nums.empty() || nums.size() < 2)
        return 0;

    int maxVal = *max_element(nums.begin(), nums.end());

    int exp = 1;                                 // 1, 10, 100, 1000 ...
    int radix = 10;                              // base 10 system

    vector<int> aux(nums.size());

    /* LSD Radix Sort */
    while (maxVal / exp > 0) {                   // Go through all digits from LSD to MSD
        vector<int> count(radix, 0);

        for (int i = 0; i < nums.size(); i++)    // Counting sort
            count[(nums[i] / exp) % 10]++;

        for (int i = 1; i < count.size(); i++)   // you could also use partial_sum()
            count[i] += count[i - 1];

        for (int i = nums.size() - 1; i >= 0; i--)
            aux[--count[(nums[i] / exp) % 10]] = nums[i];

        for (int i = 0; i < nums.size(); i++)
            nums[i] = aux[i];

        exp *= 10;
    }

    int maxGap = 0;

    for (int i = 0; i < nums.size() - 1; i++)
        maxGap = max(nums[i + 1] - nums[i], maxGap);

    return maxGap;
}

```
**复杂度分析：**
- 时间复杂度：O(n)。
- 空间复杂度：O(n)。



### 3.桶和鸽笼原理
**思路：**
```
private class Bucket {
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
}

public int maximumGap(int[] nums) {
    if (nums == null || nums.length < 2) {
        return 0;
    }

    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int i : nums) {
        min = Math.min(min, i);
        max = Math.max(max, i);
    }

    // 分配桶的长度和个数是桶排序的关键
    // 在 n 个数下，形成的两两相邻区间是 n - 1 个，比如 [2,4,6,8] 这里
    // 有 4 个数，但是只有 3 个区间，[2,4], [4,6], [6,8]
    // 因此，桶长度 = 区间总长度 / 区间总个数 = (max - min) / (nums.length - 1)
    int bucketSize = Math.max(1, (max - min) / (nums.length - 1));

    // 上面得到了桶的长度，我们就可以以此来确定桶的个数
    // 桶个数 = 区间长度 / 桶长度
    // 这里考虑到实现的方便，多加了一个桶，为什么？
    // 还是举上面的例子，[2,4,6,8], 桶的长度 = (8 - 2) / (4 - 1) = 2
    //                           桶的个数 = (8 - 2) / 2 = 3
    // 已知一个元素，需要定位到桶的时候，一般是 (当前元素 - 最小值) / 桶长度
    // 这里其实利用了整数除不尽向下取整的性质
    // 但是上面的例子，如果当前元素是 8 的话 (8 - 2) / 2 = 3，对应到 3 号桶
    //              如果当前元素是 2 的话 (2 - 2) / 2 = 0，对应到 0 号桶
    // 你会发现我们有 0,1,2,3 号桶，实际用到的桶是 4 个，而不是 3 个
    // 透过例子应该很好理解，但是如果要说根本原因，其实是开闭区间的问题
    // 这里其实 0,1,2 号桶对应的区间是 [2,4),[4,6),[6,8)
    // 那 8 怎么办？多加一个桶呗，3 号桶对应区间 [8,10)
    Bucket[] buckets = new Bucket[(max - min) / bucketSize + 1];

    for (int i = 0; i < nums.length; ++i) {
        int loc = (nums[i] - min) / bucketSize;

        if (buckets[loc] == null) {
            buckets[loc] = new Bucket();
        }

        buckets[loc].min = Math.min(buckets[loc].min, nums[i]);
        buckets[loc].max = Math.max(buckets[loc].max, nums[i]);
    }

    int previousMax = Integer.MAX_VALUE; int maxGap = Integer.MIN_VALUE;
    for (int i = 0; i < buckets.length; ++i) {
        if (buckets[i] != null && previousMax != Integer.MAX_VALUE) {
            maxGap = Math.max(maxGap, buckets[i].min - previousMax);
        }

        if (buckets[i] != null) {
            previousMax = buckets[i].max;
            maxGap = Math.max(maxGap, buckets[i].max - buckets[i].min);
        }
    }

    return maxGap;
}


```
**复杂度分析：**
- 时间复杂度：O(n)。
- 空间复杂度：O(b)。



## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/maximum-gap/solution/zui-da-jian-ju-by-leetcode/)
[MisterBooo](https://leetcode-cn.com/problems/maximum-gap/solution/mei-xiang-dao-wo-men-zhi-jian-de-zui-da-jian-ju-ji/)***
