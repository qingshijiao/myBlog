---
title: 31. 下一个排列（Next Permutation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```



# 题解

## 官方题解
### 1.字典
**思路：** 数组从后向前遍历，找到 nums[i] < nums[i + 1], 将 nums[i] 和它后面的仅大于它的数 num[j] 交换，这样 nums[i] 后面的数就是降序排列的，将其反转即可。
[LeetCode](https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-by-leetcode/)
![](https://i.loli.net/2019/09/09/HWFhAEZBiTrzgvI.png)
![](https://i.loli.net/2019/09/09/5vJyXMGnICL9mSb.png)
![](https://i.loli.net/2019/09/09/6gEhWZDAfo2lwcV.png)
![](https://i.loli.net/2019/09/09/iWvzgSMCwe1rXoF.png)
![](https://i.loli.net/2019/09/09/GIAFhnJHkYaOwNb.png)



```
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        if (i >= 0) {
            int j = nums.length - 1;
            while (j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }

    private void reverse(int[] nums, int start) {
        int i = start, j = nums.length - 1;
        while (i < j) {
            swap(nums, i, j);
            i++;
            j--;
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)，在最坏的情况下，只需要对整个数组进行两次扫描。
- 空间复杂度：O(1)，没有使用额外的空间，原地替换足以做到。

## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words)
[powcai](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/solution/chuan-lian-suo-you-dan-ci-de-zi-chuan-by-powcai/)***
