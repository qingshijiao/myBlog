s---
title: 238.除自身以外数组的乘积（Product of Array Except Self）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [238\. 除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self/)

Difficulty: **中等**


给定长度为 _n_ 的整数数组 `nums`，其中 _n_ > 1，返回输出数组 `output` ，其中 `output[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积。

**示例:**

```
输入: [1,2,3,4]
输出: [24,12,8,6]
```

**说明:** 请**不要使用除法**且在 O(_n_) 时间复杂度内完成此题。

**进阶：**
你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组**不被视为**额外空间。）


#### Solution1 - 左积与右积之双指针

Language: **Java**

```java
​public int[] productExceptSelf(int[] nums) {
        int n = nums.length-1;
        int sum = 1;
        int sumL = 1;
        int[] arr = new int[nums.length];
        for(int i=0;i<=n;i++){
            if(i>n-i){
                arr[i] = sum*arr[i];
                arr[n-i]=sumL*arr[n-i];
            }else if(i==n-i){
                arr[i] = sum*sumL;
            }else {
                arr[i]=sum;
                arr[n-i]=sumL;
            }
            sum*=nums[i];
            sumL*=nums[n-i];
        }
        return arr;
    }

```

#### Solution2 - 左积与右积之两次遍历

Language: **Java**

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length - 1;
        int sum = 1;
        int[] arr = new int[nums.length];
        for(int i=0;i<=n;i++){
            arr[i] = sum;
            sum*=nums[i];
        }
        sum = 1;
        for(int i=n;i>=0;i--){
            arr[i]*=sum;
            sum*=nums[i];
        }
        return arr;

    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/product-of-array-except-self/submissions/)
[zhangbaipeng](https://leetcode-cn.com/problems/product-of-array-except-self/solution/java-zuo-ji-you-ji-by-zhangbaipeng/)***
