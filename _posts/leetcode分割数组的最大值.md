---
title: 410.分割数组的最大值 (Split Array Largest Sum)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [409\. 最长回文串](https://leetcode-cn.com/problems/split-array-largest-sum/)

Difficulty: **困难**


给定一个非负整数数组和一个整数 _m_，你需要将这个数组分成 _m _个非空的连续子数组。设计一个算法使得这 _m _个子数组各自和的最大值最小。

**注意:**  
数组长度 _n _满足以下条件:

*   1 ≤ _n_ ≤ 1000
*   1 ≤ _m_ ≤ min(50, _n_)

**示例:**

```
输入:
nums = [7,2,5,10,8]
m = 2

输出:
18

解释:
一共有四种方法将nums分割为2个子数组。
其中最好的方式是将其分为[7,2,5] 和 [10,8]，
因为此时这两个子数组各自的和的最大值为18，在所有情况中最小。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int splitArray(int[] nums, int m) {
        long l = 0, r = Long.MAX_VALUE;
        while(l < r){
            long mid = l + (r - l) / 2;
            if(canSplit(nums, mid, m)){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        return (int)l;
    }

    private boolean canSplit(int[] nums, long target, int m){
        long sum = 0;   
        int count = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] > target) return false;
            sum += nums[i];
             if(sum > target){
                 count++;
                 if(count >= m){
                     return false;
                 }
                 sum = nums[i];
             }
        }
       // if(sum > target) return false;
        return true;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/split-array-largest-sum/submissions/)***
