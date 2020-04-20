---
title: 368.最大整除子集 (Largest Divisible Subset)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [368\. 最大整除子集](https://leetcode-cn.com/problems/largest-divisible-subset/)

Difficulty: **中等**


给出一个由**无重复的**正整数组成的集合，找出其中最大的整除子集，子集中任意一对 (S<sub style="display: inline;">i，</sub>S<sub style="display: inline;">j</sub>) 都要满足：S<sub style="display: inline;">i</sub> % S<sub style="display: inline;">j</sub> = 0 或 S<sub style="display: inline;">j</sub> % S<sub style="display: inline;">i</sub> = 0。

如果有多个目标子集，返回其中任何一个均可。

**示例 1:**

```
输入: [1,2,3]
输出: [1,2] (当然, [1,3] 也正确)
```

**示例 2:**

```
输入: [1,2,4,8]
输出: [1,2,4,8]
```


#### Solution

Language: **Java**

```java
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
      List<Integer> ans=new ArrayList<>();
        if (nums.length==0){
            return ans;
        }
        int[] dp=new int[nums.length];
        int[] dp2=new int[nums.length];
        Arrays.fill(dp,1);
        Arrays.fill(dp2,-1);
        Arrays.sort(nums);
        for (int i=1;i<nums.length;i++){
            for (int j=0;j<i;j++){
                if (nums[i]%nums[j]==0){
                    if (dp[i]<dp[j]+1){
                        dp[i]=dp[j]+1;
                        dp2[i]=j;
                    }
                }
            }
        }
        int index=0;
        for (int i=1;i<nums.length;i++){
            if (dp[i]>dp[index]){
                index=i;
            }
        }
        while (index!=-1){
            ans.add(nums[index]);
            index=dp2[index];
        }
        return ans;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/largest-divisible-subset/solution/zui-da-zheng-chu-zi-ji-by-leetcode/)***
