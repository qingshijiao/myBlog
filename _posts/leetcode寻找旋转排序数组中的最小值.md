---
title: 153.寻找旋转排序数组中的最小值（Find Minimum in Rotated Sorted Array）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

示例 1:
```
输入: [3,4,5,1,2]
输出: 1
```
示例 2:
```
输入: [4,5,6,7,0,1,2]
输出: 0
```

# 题解

## 官方题解
## 1.二分
**思路：**
```
class Solution {
  public int findMin(int[] nums) {
    // If the list has just one element then return that element.
    if (nums.length == 1) {
      return nums[0];
    }

    // initializing left and right pointers.
    int left = 0, right = nums.length - 1;

    // if the last element is greater than the first element then there is no rotation.
    // e.g. 1 < 2 < 3 < 4 < 5 < 7. Already sorted array.
    // Hence the smallest element is first element. A[0]
    if (nums[right] > nums[0]) {
      return nums[0];
    }

    // Binary search way
    while (right >= left) {
      // Find the mid element
      int mid = left + (right - left) / 2;

      // if the mid element is greater than its next element then mid+1 element is the smallest
      // This point would be the point of change. From higher to lower value.
      if (nums[mid] > nums[mid + 1]) {
        return nums[mid + 1];
      }

      // if the mid element is lesser than its previous element then mid element is the smallest
      if (nums[mid - 1] > nums[mid]) {
        return nums[mid];
      }

      // if the mid elements value is greater than the 0th element this means
      // the least value is still somewhere to the right as we are still dealing with elements
      // greater than nums[0]
      if (nums[mid] > nums[0]) {
        left = mid + 1;
      } else {
        // if nums[0] is greater than the mid value then this means the smallest value is somewhere to
        // the left
        right = mid - 1;
      }
    }
    return -1;
  }
}

```

```
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = (left + right) >> 1;
            if (nums[mid] < nums[right]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return nums[left];
    }
}
```
**复杂度分析：**
- 时间复杂度：和二分搜索一样 O(logN)
- 空间复杂度：O(1)

## 其他题解
### 1.分治
**思路：**


```
public class Solution {

    // 虽然可以通过，但是时间复杂度是 O(n)

    public int findMin(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            throw new IllegalArgumentException("数组为空");
        }
        return findMin(nums, 0, len - 1);
    }

    private int findMin(int[] nums, int left, int right) {
        // 思考：这个临界条件是为什么?
        // 或者写成 left + 1 >= right
        if (left == right || left + 1 == right) {
            return Math.min(nums[left], nums[right]);
        }
        // int mid = left + (right - left) / 2;
        int mid = (left + right) >>> 1;
        // 8 9 1 2 3 4 5 6 7
        if (nums[mid] < nums[right]) {
            // 右边是顺序数组
            return Math.min(findMin(nums, left, mid - 1), nums[mid]);
        } else {
            // 左边是顺序数组
            // nums[mid] > nums[right]
            // 3 4 5 6 7 8 1 2
            return Math.min(nums[left], findMin(nums, mid + 1, right));
        }
    }

    public static void main(String[] args) {
        Solution2 solution2 = new Solution2();
        int[] nums = {1, 2};
        int solution2Min = solution2.findMin(nums);
        System.out.println(solution2Min);
    }

}


```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/xun-zhao-xuan-zhuan-pai-lie-shu-zu-zhong-de-zui-xi/)
[powcai](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/er-fen-fa-fen-zhi-fa-python-dai-ma-java-dai-ma-by-/)***
