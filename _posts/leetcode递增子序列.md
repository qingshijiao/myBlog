---
title: 491. 递增子序列 (Increasing Subsequences)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [491\. 递增子序列](https://leetcode-cn.com/problems/increasing-subsequences/)

Difficulty: **中等**


给定一个整型数组, 你的任务是找到所有该数组的递增子序列，递增子序列的长度至少是2。

**示例:**

```
输入: [4, 6, 7, 7]
输出: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

**说明:**

1.  给定数组的长度不会超过15。
2.  数组中的整数范围是 [-100,100]。
3.  给定数组中可能包含重复数字，相等的数字应该被视为递增的一种情况。


#### Solution

Language: **Java**

```java
class Solution {
    public List<List<Integer>> ret=new ArrayList();
    public List<List<Integer>> findSubsequences(int[] nums) {
        help(0,nums,new ArrayList<Integer>());
        return ret;
    }
    private void help(int i,int[] nums,ArrayList list){
        if(i>=nums.length){
            if(list.size()>=2)
            ret.add(new ArrayList(list));
            return;
        }                   
        if(list.size()==0||nums[i]>=(int)list.get(list.size()-1)){           
            list.add(nums[i]);
            help(i+1,nums,list);
            list.remove(list.size()-1);
        }
        if(i>0&&list.size()!=0&&nums[i]==(int)list.get(list.size()-1))
            return ;        
           help(i+1,nums,list); 
                                 
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/increasing-subsequences/)***
