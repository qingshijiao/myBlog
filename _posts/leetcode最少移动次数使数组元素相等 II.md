---
title: 462. 最少移动次数使数组元素相等 II (Minimum Moves to Equal Array Elements II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [462\. 最少移动次数使数组元素相等 II](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements-ii/)

Difficulty: **中等**


给定一个非空整数数组，找到使所有数组元素相等所需的最小移动数，其中每次移动可将选定的一个元素加1或减1。 您可以假设数组的长度最多为10000。

**例如:**

```
输入:
[1,2,3]

输出:
2

说明：
只有两个动作是必要的（记得每一步仅可使其中一个元素加1或减1）： 

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int minMoves2(int[] nums) {
        int i=0,j=nums.length-1;
        int ret=0;
        Arrays.sort(nums);
        while(i<j){
            ret+=nums[j]-nums[i];
            i++;
            j--;
        }
        return ret;
    }
}
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements-ii/)***
