---
title: 487.最大连续1的个数之二（Max Consecutive Ones II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

Example 1:

Input: [1,0,1,1,0]
Output: 4
Explanation: Flip the first zero will get the the maximum number of consecutive 1s.
    After flipping, the maximum number of consecutive 1s is 4.
 

Note:

The input array will only contain 0 and 1.
The length of input array is a positive integer and will not exceed 10,000
 

Follow up:
What if the input numbers come in one by one as an infinite stream? In other words, you can't store all numbers coming from the stream as it's too large to hold in memory. Could you solve it efficiently?


#### Solution

Language: **c++**

```c++
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int res = 0, left = 0, k = 1;
        queue<int> q;
        for (int right = 0; right < nums.size(); ++right) {
            if (nums[right] == 0) q.push(right);
            if (q.size() > k) {
                left = q.front() + 1; q.pop();
            }
            res = max(res, right - left + 1);
        }
        return res;
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6376115.html)***
