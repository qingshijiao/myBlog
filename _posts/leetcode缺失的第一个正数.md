---
title: 41. 缺失的第一个正数（First Missing Positive）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

示例 1:
```
输入: [1,2,0]
输出: 3
```
示例 2:
```
输入: [3,4,-1,1]
输出: 2
```
示例 3:
```
输入: [7,8,9,11,12]
输出: 1
```
**说明:**
你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间。


# 题解

## 官方题解
### 1.索引作为哈希键值
**思路：** 使用索引作为哈希键 以及 元素的符号作为哈希值 来实现是否存在的检测。
> "脏工作环境" 的解决方法是将一个字符串 hash_str 分配 n 个 0，并且用类似于哈希表的方法，如果在数组中出现数字 i 则将字符串中 hash_str[i] 修改为 1 。

- 这一个数组中如果存在某一个数，我们将其作为索引，然后改变其索引对应的值。比如我们遍历到 nums[i] = m, 我们将 m 作为索引，将其对应元素改变符号，nums[m] = -nums[m]，重复元素只变化一次。
- 我们可以先遍历一遍将 0 和负数（这些是没有用的）都变成 1，这样只要对应元素是负值，我们就认为其存在在数组中。
- 为了 1 冲突，我们先遍历一遍，看 1 是否存在。

```
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;

        // 基本情况
        int contains = 0;
        for (int i = 0; i < n; i++)
          if (nums[i] == 1) {
            contains++;
            break;
          }

        if (contains == 0)
          return 1;

        // nums = [1]
        if (n == 1)
          return 2;

        // 用 1 替换负数，0，和大于 n 的数
        // 在转换以后，nums 只会包含正数
        for (int i = 0; i < n; i++)
          if ((nums[i] <= 0) || (nums[i] > n))
            nums[i] = 1;

        // 使用索引和数字符号作为检查器
        // 例如，如果 nums[1] 是负数表示在数组中出现了数字 `1`
        // 如果 nums[2] 是正数 表示数字 2 没有出现
        for (int i = 0; i < n; i++) {
          int a = Math.abs(nums[i]);
          // 如果发现了一个数字 a - 改变第 a 个元素的符号
          // 注意重复元素只需操作一次
          if (a == n)
            nums[0] = - Math.abs(nums[0]);
          else
            nums[a] = - Math.abs(nums[a]);
        }

        // 现在第一个正数的下标
        // 就是第一个缺失的数
        for (int i = 1; i < n; i++) {
          if (nums[i] > 0)
            return i;
        }

        if (nums[0] > 0)
          return n;

        return n + 1;
  }
}
```
**复杂度分析**
- 时间复杂度： O(N) 由于所有的操作一共只会遍历长度为 N 的数组 4 次。
- 空间复杂度： O(1) 由于只使用了常数的空间。


## 其他题解
### 1.桶排序 + 异或交换
**思路：** 将正元素值放到其对应位置，值不匹配的说明这个数不存在
![](https://i.loli.net/2019/09/14/dy1hbIxKN2lrQ4E.png)

```
class Solution {
    public int firstMissingPositive(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            while (nums[i] > 0 && nums[i] <= len && nums[nums[i] - 1] != nums[i]) {
                swap(nums, nums[i] - 1, i);
            }
        }
        for (int i = 0; i < len; i++) {
            if (nums[i] - 1 != i) {
                return i + 1;
            }
        }
        return len + 1;
    }

    private void swap(int[] nums, int index1, int index2) {
        if (index1 == index2) {
            return;
        }
        nums[index1] = nums[index1] ^ nums[index2];
        nums[index2] = nums[index1] ^ nums[index2];
        nums[index1] = nums[index1] ^ nums[index2];
    }
}
```
**复杂度分析**
- 时间复杂度： O(N)，这里 N 是数组的长度，其实只要看这个数组一遍，就可以知道每个数字应该放在哪个位置，所以时间复杂度是 O(N)。。
- 空间复杂度： O(1)，桶排序在原地进行，没有使用额外的存储空间。。



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/first-missing-positive/solution/que-shi-de-di-yi-ge-zheng-shu-by-leetcode/)
[liweiwei1419](https://leetcode-cn.com/problems/first-missing-positive/solution/tong-pai-xu-python-dai-ma-by-liweiwei1419/)***
