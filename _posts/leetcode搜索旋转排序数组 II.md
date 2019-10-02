---
title: 81.搜索旋转排序数组 II (Search in Rotated Sorted Array II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

示例 1:
```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```
示例 2:
```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```
**进阶:**

- 这是 搜索旋转排序数组 的延伸题目，本题中的 nums  可能包含重复元素。
- 这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？


# 题解

## 官方题解
暂无

## 其他题解
### 1.利用建堆的思想
**思想：** 实现了超快的执行速度，但是内存消耗也是非常大的

```
class Solution {
    public boolean search(int[] nums, int target) {
        int i;

        if(nums.length == 0)
            return false;

        for(i=0; i<=nums.length/2; i++){
            if(nums[i] == target)
                return true;
            if(2*i+1<=nums.length-1 && nums[2*i+1] == target)
                return true;
            if(2*i+2<=nums.length-1 && nums[2*i+2] == target)
                return true;
        }
        return false;
    }
}
```


### 2.二分查找
**思想：**

```
class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[start] == nums[mid]) {
                start++;
                continue;
            }
            //前半部分有序
            if (nums[start] < nums[mid]) {
                //target在前半部分
                if (nums[mid] > target && nums[start] <= target) {
                    end = mid - 1;
                } else {  //否则，去后半部分找
                    start = mid + 1;
                }
            } else {
                //后半部分有序
                //target在后半部分
                if (nums[mid] < target && nums[end] >= target) {
                    start = mid + 1;
                } else {  //否则，去后半部分找
                    end = mid - 1;

                }
            }
        }
        //一直没找到，返回false
        return false;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/submissions/)
[le-er-you-you](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/solution/java-li-yong-jian-dui-de-si-xiang-chao-kuai-shi-xi/)
[reedfan](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/solution/zai-javazhong-ji-bai-liao-100de-yong-hu-by-reedfan/)***
