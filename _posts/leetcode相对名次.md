---
title: 506. 相对名次（Relative Ranks）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [506\. 相对名次](https://leetcode-cn.com/problems/relative-ranks/)

Difficulty: **简单**


给出 **N** 名运动员的成绩，找出他们的相对名次并授予前三名对应的奖牌。前三名运动员将会被分别授予 “金牌”，“银牌” 和“ 铜牌”（"Gold Medal", "Silver Medal", "Bronze Medal"）。

(注：分数越高的选手，排名越靠前。)

**示例 1:**

```
输入: [5, 4, 3, 2, 1]
输出: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
解释: 前三名运动员的成绩为前三高的，因此将会分别被授予 “金牌”，“银牌”和“铜牌” ("Gold Medal", "Silver Medal" and "Bronze Medal").
余下的两名运动员，我们只需要通过他们的成绩计算将其相对名次即可。
```

**提示:**

1.  N 是一个正整数并且不会超过 10000。
2.  所有运动员的成绩都不相同。


#### Solution

Language: **Java**

```java
class Solution {
    public String[] findRelativeRanks(int[] nums) {
        //结果数组
        String[] result = new String[nums.length];
        //遍历数组找到最大值
        int max = 0;
        for(int i=0;i<nums.length;i++){
            max = Math.max(max,nums[i]);
        }
        //构造一个数组
        int[] help = new int[max+1];
        //数组下标为0~max个元素值，下标上存储的是该元素值在nums元素中的对应下标+1(不加1的话就会有0，和后面不存在的情况分不开了)，如果不存在就是0
        for(int i=0;i<nums.length;i++){
            help[nums[i]] = i+1;
        }
        //然后倒着遍历Help数组，下标对应从大到小的元素，数组值为nums下标值+1
        for(int i=max,flag = 1;i>=0;i--){
            //如果是0的话，说明nums里不存在i这个元素，跳过
            if(help[i]>0){
                switch(flag){
                    case 1: result[help[i]-1] = "Gold Medal";break;
                    case 2: result[help[i]-1] = "Silver Medal";break;
                    case 3: result[help[i]-1] = "Bronze Medal";break;
                    default: result[help[i]-1] = Integer.toString(flag);
                }
                flag++;
            }
        }
        return result;

    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/relative-ranks/)***
