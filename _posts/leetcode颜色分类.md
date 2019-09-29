---
title: 75. 颜色分类（Sort Colors）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

**注意:**
不能使用代码库中的排序函数来解决这道题。

示例:
```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```

**进阶：**

- 一个直观的解决方案是使用计数排序的两趟扫描算法。
- 首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
- 你能想出一个仅使用常数空间的一趟扫描算法吗？


# 题解

## 官方题解
### 1.双指针
**思路：**
![](https://pic.leetcode-cn.com/3ab6cc20bb91835c2722c688c2f894e407289333bae839a930957461e810a957-image.png)

![](https://pic.leetcode-cn.com/fe866418cf2c4a3f952e306244154bedf08de877cd32c90a3360037083f824f3-image.png)
![](https://pic.leetcode-cn.com/cf9424fc35b46c2cc22245bcabd1a6c9174b45330fa3583ad1d0b7ffccd24467-image.png)
![](https://pic.leetcode-cn.com/37d97fa81e2a9c8c745792aea95cb4662a1e3b8995f56ec6cccd2f24ab7c6376-image.png)

```
class Solution {
  /*
  荷兰三色旗问题解
  */
  public void sortColors(int[] nums) {
    // 对于所有 idx < i : nums[idx < i] = 0
    // j是当前考虑元素的下标
    int p0 = 0, curr = 0;
    // 对于所有 idx > k : nums[idx > k] = 2
    int p2 = nums.length - 1;

    int tmp;
    while (curr <= p2) {
      if (nums[curr] == 0) {
        // 交换第 p0个和第curr个元素
        // i++，j++
        tmp = nums[p0];
        nums[p0++] = nums[curr];
        nums[curr++] = tmp;
      }
      else if (nums[curr] == 2) {
        // 交换第k个和第curr个元素
        // p2--
        tmp = nums[curr];
        nums[curr] = nums[p2];
        nums[p2--] = tmp;
      }
      else curr++;
    }
  }
}
```
**复杂度分析：**
- 时间复杂度：由于对长度 N的数组进行了一次遍历，时间复杂度为O(N) 。
- 空间复杂度：由于只使用了常数空间，空间复杂度为O(1) 。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/sort-colors/solution/yan-se-fen-lei-by-leetcode/)***
