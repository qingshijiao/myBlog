---
title: 448. 找到所有数组中消失的数字 (Find All Numbers Disappeared in an Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [448\. 找到所有数组中消失的数字](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

Difficulty: **简单**


给定一个范围在  1 ≤ a[i] ≤ _n_ ( _n_ = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, _n_] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为_O(n)_的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

**示例:**

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        boolean[] flag = new boolean[nums.length + 1];
        for(int num : nums) {
            flag[num] = true;
        } 
        for(int i = 1;i < flag.length;i++) {
            if(flag[i] == false) res.add(i);
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/submissions/)***
