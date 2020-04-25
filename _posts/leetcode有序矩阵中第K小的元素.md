---
title: 378.有序矩阵中第K小的元素 (Kth Smallest Element in a Sorted Matrix)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [378\. 有序矩阵中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)

Difficulty: **中等**


给定一个 _n x n _矩阵，其中每行和每列元素均按升序排序，找到矩阵中第k小的元素。
请注意，它是排序后的第 k 小元素，而不是第 k 个不同的元素。

**示例:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。
```

**提示：**
你可以假设 k 的值永远是有效的, 1 ≤ k ≤ n<sup>2 </sup>。


#### Solution

Language: **Java**

```java
​class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int left = matrix[0][0], right = matrix[n-1][n-1];
        while(left < right) {
            int mid = left + ((right - left) >> 1);
            int cnt = countLessThan(matrix, mid);
            // mid 可能不是数组中的数字，不能直接判断cnt==k返回mid
            if (cnt < k) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }

    private int countLessThan(int[][] matrix, int num) {
        int n = matrix.length;
        int i = n - 1, j = 0, count = 0;
        while(i >= 0 && j < n) {
            if (matrix[i][j] <= num) {
                count += i + 1;
                j ++;
            } else {
                i --;
            }
        }
        return count ;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/submissions/)***
