---
title: 57. 插入区间（Insert Interval）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

示例 1:
```
输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
输出: [[1,5],[6,9]]
```
示例 2:
```
输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出: [[1,2],[3,10],[12,16]]
解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.双指针
**思路：** 先排序，后合并数组
```
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        //双指针记录左指针的位置
        int recordFirst = newInterval[0];
        //右指针
        int recordTwo = newInterval[1];
        //两个指针的位置只可能在区间中或者在区间外
        List<int[]> result = new ArrayList<>();
        int i = 0;
        //定位左指针的位置
        for(;i<intervals.length;i++){
            ////如果大于右区间，则与下一个区间比对，并记录当前区间的值
            if(recordFirst > intervals[i][1]){
                result.add(intervals[i]);
                continue;
            }else{
                //判断在区间外还是在区间内
                if(recordFirst<intervals[i][0]){
                    break;
                }else{
                    recordFirst = intervals[i][0];
                    break;
                }

            }
        }
        //定位右指针的位置
         for(;i<intervals.length;i++){
             //同理
            if(recordTwo > intervals[i][1]){
                continue;
            }else{
                 if(recordTwo<intervals[i][0]){
                    break;
                }else{
                     //如果右指针在区间内，则此区间则不需要被记录了，所以i++
                    recordTwo = intervals[i][1];
                     i++;
                    break;
                }
            }
         }
        //记录左右指针
        int[] temp = {recordFirst,recordTwo};
        result.add(temp);
        //如果后面还有，则继续记录
        for(;i<intervals.length;i++){
             result.add(intervals[i]);
        }
        int[][] finalResult = new int[result.size()][2];
        for(int j = 0;j<finalResult.length;j++){
            finalResult[j] = result.get(j);
        }
        return finalResult;
    }

}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/insert-interval/submissions/)***
