---
title: 373.查找和最小的K对数字 (Find K Pairs with Smallest Sums)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [373\. 查找和最小的K对数字](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/)

Difficulty: **中等**


给定两个以升序排列的整形数组 **nums1** 和 **nums2**, 以及一个整数 **k**。

定义一对值 **(u,v)**，其中第一个元素来自 **nums1**，第二个元素来自 **nums2**。

找到和最小的 k 对数字 **(u<sub style="display: inline;">1</sub>,v<sub style="display: inline;">1</sub>), (u<sub style="display: inline;">2</sub>,v<sub style="display: inline;">2</sub>) ... (u<sub style="display: inline;">k</sub>,v<sub style="display: inline;">k</sub>)**。

**示例 1:**

```
输入: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
输出: [1,2],[1,4],[1,6]
解释: 返回序列中的前 3 对数：
     [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

**示例 2:**

```
输入: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
输出: [1,1],[1,1]
解释: 返回序列中的前 2 对数：
     [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

**示例 3:**

```
输入: nums1 = [1,2], nums2 = [3], k = 3
输出: [1,3],[2,3]
解释: 也可能序列中所有的数对都被返回:[1,3],[2,3]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        int n1 = nums1.length;
        int n2 = nums2.length;
        if(k==0 || n1 == 0 || n2 == 0) return res;
        //下标代表nums1的下标，值代表nums2的下标
        int[] d = new int[nums1.length];
        int n = 0;//记录有几个元素已经用完了
        //当到底k个或者没有元素可用退出循环
        while(k>0 && n<n1){
            int min = Integer.MAX_VALUE;
            int min1 = -1;
            for(int i = n;i<nums1.length;i++){
                //当对应的nums2中的第一个，则只会越来越大， 没必要继续了。系数肯定是递增的关系
                if(i > 0 && d[i-1]==0) break;
                //因为d[i]代表nums2的下标，所以不可能大于n2.
                if(d[i]<n2 && nums1[i]+nums2[d[i]]<min){//和比最小值小
                    min = nums1[i]+nums2[d[i]];
                    min1 = i;
                }
            }
            List<Integer> list = new ArrayList<Integer>();
            list.add(nums1[min1]);
            list.add(nums2[d[min1]]);
            res.add(list);
            d[min1]++;
            //说明这个数跟对面都匹配完了，
            if(d[min1]==n2) n++;
            k--;
        }
        return res;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/submissions/)***
