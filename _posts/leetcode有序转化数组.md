---
title: 360.有序转化数组 (Sort Transformed Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a sorted array of integers nums and integer values a, b and c. Apply a function of the form f(x) = ax2 + bx + c to each element x in the array.

The returned array must be in sorted order.

Expected time complexity: O(n)

Example:
```
nums = [-4, -2, 2, 4], a = 1, b = 3, c = 5,

Result: [3, 9, 15, 33]

nums = [-4, -2, 2, 4], a = -1, b = 3, c = 5

Result: [-23, -5, 1, 7]
```
**Credits:**

Special thanks to @elmirap for adding this problem and creating all test cases.

#### Solution

Language: **Java**

```java
public class Solution {
    private int calcu(int x, int a, int b, int c){
        return a*x*x + b*x + c;
    }


    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int index;
        if(a > 0){
            index = nums.length - 1 ;
        } else {
            index = 0;
        }
        int result[] = new int[nums.length];
        int i = 0;
        int j = nums.length - 1;
        if(a > 0){
            while(i <= j){
                result[index--] = calcu(nums[i],a,b,c) > calcu(nums[j],a,b,c) ? calcu(nums[i++],a,b,c):calcu(nums[j--],a,b,c);
            }
        }else{
            while(i <= j){
                result[index++] = calcu(nums[i],a,b,c) < calcu(nums[j],a,b,c) ? calcu(nums[i++],a,b,c):calcu(nums[j--],a,b,c);
            }
        }
        return result;
    }
}　
```
---
***参考:
[lightwindy](https://www.cnblogs.com/lightwindy/p/9723290.html)***
