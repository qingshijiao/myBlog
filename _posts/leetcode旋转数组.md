---
title: 189.旋转数组（Rotate Array）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [189\. 旋转数组](https://leetcode-cn.com/problems/rotate-array/)

Difficulty: **简单**


给定一个数组，将数组中的元素向右移动 _k _个位置，其中 _k _是非负数。

**示例 1:**

```
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释:
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

**说明:**

*   尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
*   要求使用空间复杂度为 O(1) 的 **原地 **算法。


#### Solution1 - 暴力

Language: **Java**


```java
​public class Solution {
    public void rotate(int[] nums, int k) {
        int temp, previous;
        for (int i = 0; i < k; i++) {
            previous = nums[nums.length - 1];
            for (int j = 0; j < nums.length; j++) {
                temp = nums[j];
                nums[j] = previous;
                previous = temp;
            }
        }
    }
}

```
time:O(n∗k) space:O(1)

#### Solution2 - 使用额外的数组

Language: **Java**


```java
​public class Solution {
    public void rotate(int[] nums, int k) {
        int[] a = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            a[(i + k) % nums.length] = nums[i];
        }
        for (int i = 0; i < nums.length; i++) {
            nums[i] = a[i];
        }
    }
}
```
time:O(n) space:O(n)

#### Solution3 - 使用额外的数组
![](https://pic.leetcode-cn.com/f0493a97cdb7bc46b37306ca14e555451496f9f9c21effcad8517a81a26f30d6-image.png)
Language: **Java**


```java
​public class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int count = 0;
        for (int start = 0; count < nums.length; start++) {
            int current = start;
            int prev = nums[start];
            do {
                int next = (current + k) % nums.length;
                int temp = nums[next];
                nums[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }
}

```
time:O(n) space:O(1)

#### Solution4 - 使用反转

Language: **Java**


```java
​public class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}

```
time:O(n) space:O(1)


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/rotate-array/submissions/)***
