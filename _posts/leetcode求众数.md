---
title: 169.求众数（Majority Element）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

示例 1:
```
输入: [3,2,3]
输出: 3
```
示例 2:
```
输入: [2,2,1,1,1,2,2]
输出: 2
```

# 题解

## 官方题解
### 1.暴力
我们可以在平方级的时间里穷举所有情况，来检测每个数是不是众数。
```
class Solution {
    public int majorityElement(int[] nums) {
        int majorityCount = nums.length/2;

        for (int num : nums) {
            int count = 0;
            for (int elem : nums) {
                if (elem == num) {
                    count += 1;
                }
            }

            if (count > majorityCount) {
                return num;
            }

        }

        return -1;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n^2)
- 空间复杂度：O(1)


### 2.哈希表
```
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            }
            else {
                counts.put(num, counts.get(num)+1);
            }
        }
        return counts;
    }

    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);

        Map.E***y<Integer, Integer> majorityE***y = null;
        for (Map.E***y<Integer, Integer> e***y : counts.e***ySet()) {
            if (majorityE***y == null || e***y.getValue() > majorityE***y.getValue()) {
                majorityE***y = e***y;
            }
        }

        return majorityE***y.getKey();
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)
- 空间复杂度：O(n)


### 3.排序
```
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}


```
**复杂度分析：**
- 时间复杂度：O(nlgn)
- 空间复杂度：O(1) 或 O(n)

### 4.随机化
```
class Solution {
    private int randRange(Random rand, int min, int max) {
        return rand.nextInt(max - min) + min;
    }

    private int countOccurences(int[] nums, int num) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    public int majorityElement(int[] nums) {
        Random rand = new Random();

        int majorityCount = nums.length/2;

        while (true) {
            int candidate = nums[randRange(rand, 0, nums.length)];
            if (countOccurences(nums, candidate) > majorityCount) {
                return candidate;
            }
        }
    }
}

```
**复杂度分析：**
- 时间复杂度：O(无穷)
- 空间复杂度：O(1)

### 5.分治
```
class Solution {
    private int countInRange(int[] nums, int num, int lo, int hi) {
        int count = 0;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    private int majorityEleme***ec(int[] nums, int lo, int hi) {
        // base case; the only element in an array of size 1 is the majority
        // element.
        if (lo == hi) {
            return nums[lo];
        }

        // recurse on left and right halves of this slice.
        int mid = (hi-lo)/2 + lo;
        int left = majorityEleme***ec(nums, lo, mid);
        int right = majorityEleme***ec(nums, mid+1, hi);

        // if the two halves agree on the majority element, return it.
        if (left == right) {
            return left;
        }

        // otherwise, count each element and return the "winner".
        int leftCount = countInRange(nums, left, lo, hi);
        int rightCount = countInRange(nums, right, lo, hi);

        return leftCount > rightCount ? left : right;
    }

    public int majorityElement(int[] nums) {
        return majorityEleme***ec(nums, 0, nums.length-1);
    }
}


```
**复杂度分析：**
- 时间复杂度：O(nlgn)
- 空间复杂度：O(lgn)

### 6.Boyer-Moore 投票算法
```
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)
- 空间复杂度：O(1)

## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/majority-element/solution/qiu-zhong-shu-by-leetcode-2/)***
