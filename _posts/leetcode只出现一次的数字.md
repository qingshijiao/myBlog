---
title: 136.只出现一次的数字（Single Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```


# 题解

## 官方题解
### 1.数学
**思路：** 利用 set 去重特性
2∗(a+b+c)−(a+a+b+b+c)=c

## 其他题解
### 1.暴力法
**思路：** 两遍循环，每次从数组中取一个数，记为cur，然后从剩下的数中查找，如果找不到，则cur即为要找的那个数。这种解法时间复杂度是 O(n^2)

### 2.快速排序
**思路：** 使用快排，复杂度 O(nlogn)

### 3.哈希表
**思路：** 利用 Hash 表，Time: O(n) Space: O(n)

```
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (Integer i : nums) {
            Integer count = map.get(i);
            count = count == null ? 1 : ++count;
            map.put(i, count);
        }
        for (Integer i : map.keySet()) {
            Integer count = map.get(i);
            if (count == 1) {
                return i;
            }
        }
        return -1; // can't find it.
    }
}
```

### 4.异或
**思路：**

```
class Solution {
    public int singleNumber(int[] nums) {
      int ans = nums[0];
      if (nums.length > 1) {
       for (int i = 1; i < nums.length; i++) {
          ans = ans ^ nums[i];
       }
      }
      return ans;
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/single-number/solution/zhi-chu-xian-yi-ci-de-shu-zi-by-leetcode/)
[yinyinnie](https://leetcode-cn.com/problems/single-number/solution/xue-suan-fa-jie-guo-xiang-dui-yu-guo-cheng-bu-na-y/)***
