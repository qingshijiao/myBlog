---
title: 137.只出现一次的数字 II（Single Number II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,3,2]
输出: 3
```
示例 2:
```
输入: [0,1,0,1,0,1,99]
输出: 99
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.模拟三进制
**思路：**
![](https://pic.leetcode-cn.com/63eb0f2c06f289701416eaee46a40ee56e4b685fff2b1c55ad16b00fadf3c8c8-Picture16.png)

```
class Solution {
    public int singleNumber(int[] nums) {
        int ones = 0, twos = 0;
        for(int num : nums){
            ones = ones ^ num & ~twos;
            twos = twos ^ num & ~ones;
        }
        return ones;
    }
}
```

### 2.HashMap 计数
**思路：**

### 3.位操作
**思路：**
```
假如例子是 1 2 6 1 1 2 2 3 3 3, 3 个 1, 3 个 2, 3 个 3,1 个 6
1 0 0 1
2 0 1 0
6 1 1 0
1 0 0 1
1 0 0 1
2 0 1 0
2 0 1 0
3 0 1 1
3 0 1 1
3 0 1 1
看最右边的一列 1001100111 有 6 个 1
再往前看一列 0110011111 有 7 个 1
再往前看一列 0010000 有 1 个 1
我们只需要把是 3 的倍数的对应列写 0，不是 3 的倍数的对应列写 1
也就是 1 1 0,也就是 6。
```

```
public int singleNumber(int[] nums) {
    int ans = 0;
    //考虑每一位
    for (int i = 0; i < 32; i++) {
        int count = 0;
        //考虑每一个数
        for (int j = 0; j < nums.length; j++) {
            //当前位是否是 1
            if ((nums[j] >>> i & 1) == 1) {
                count++;
            }
        }
        //1 的个数是否是 3 的倍数
        if (count % 3 != 0) {
            ans = ans | 1 << i;
        }
    }
    return ans;
}
```




---
***参考：
[LeetCode](https://leetcode-cn.com/problems/single-number-ii/submissions/)
[jyd](https://leetcode-cn.com/problems/single-number-ii/solution/single-number-ii-mo-ni-san-jin-zhi-fa-by-jin407891/)
[windliang](https://leetcode-cn.com/problems/single-number-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--31/)***
