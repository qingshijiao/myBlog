---
title: 347.前 K 个高频元素 (Top K Frequent Elements)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [347\. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

Difficulty: **中等**


给定一个非空的整数数组，返回其中出现频率前 **_k _**高的元素。

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

**说明：**

*   你可以假设给定的 _k _总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
*   你的算法的时间复杂度**必须**优于 O(_n_ log _n_) , _n _是数组的大小。


#### Solution

Language: **Java**

```java
​class Solution {
    //前 K 个高频元素
     public List<Integer> topKFrequent(int[] nums, int k) {
    	 List<Integer> list=new ArrayList();
    	 Arrays.sort(nums);
    	 int distinctLen=1;
    	 for(int i=1;i<nums.length;i++){
    		 if(nums[i]!=nums[i-1]){
    			 distinctLen++;
    		 }
    	 }
    	 int counts[]=new int[distinctLen];
    	 int order[]=new int[distinctLen];
    	 int index=0;
    	 int count=1;
    	 for(int i=1;i<nums.length;i++){
    		 if(nums[i]==nums[i-1]){
    			 count++;
    		 }else{
    			 counts[index]=count;
    			 order[index]=count;
    			 nums[index]=nums[i-1];
    			 index++;
    			 count=1;
    		 }
    	 }
    	 nums[index]=nums[nums.length-1];
    	 counts[index]=count;
    	 order[index]=count;
    	 Arrays.sort(order);
    	 int kth=order[distinctLen-k];
    	 for(int i=0;i<=index;i++){
    		 if(counts[i]>=kth){
    			 list.add(nums[i]);
    		 }
    	 }
    	 return list;
     }
}
```

---
***参考:
[jmspan](https://leetcode-cn.com/problems/top-k-frequent-elements/submissions/)***
