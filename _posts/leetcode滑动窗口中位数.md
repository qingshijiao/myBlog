---
title: 480. 滑动窗口中位数（Sliding Window Median）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [480\. 滑动窗口中位数](https://leetcode-cn.com/problems/sliding-window-median/)

Difficulty: **困难**


中位数是有序序列最中间的那个数。如果序列的大小是偶数，则没有最中间的数；此时中位数是最中间的两个数的平均数。

例如：

*   `[2,3,4]`，中位数是 `3`
*   `[2,3]`，中位数是 `(2 + 3) / 2 = 2.5`

给你一个数组 _nums_，有一个大小为 _k_ 的窗口从最左端滑动到最右端。窗口中有 _k_ 个数，每次窗口向右移动 _1_ 位。你的任务是找出每次窗口移动后得到的新窗口中元素的中位数，并输出由它们组成的数组。

**示例：**

给出 _nums_ = `[1,3,-1,-3,5,3,6,7]`，以及 _k_ = 3。

```
窗口位置                      中位数
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7      -1
 1  3 [-1  -3  5] 3  6  7      -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6
```

 因此，返回该滑动窗口的中位数数组 `[1,-1,-1,3,5,6]`。

**提示：**

*   你可以假设 `k` 始终有效，即：`k` 始终小于输入的非空数组的元素个数。
*   与真实值误差在 `10 ^ -5` 以内的答案将被视作正确答案。


#### Solution

Language: **Java**

```java
​class Solution {
    // 考察快排寻找第i个元素
    public double[] medianSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        double[] res = new double[n - k + 1];
        TreeNode root = null;
        
        int resIdx = 0;
        
        for (int i = 0; i < nums.length; i++) {
            root = add(root, nums[i]);
            if (i < k - 1) continue;
            if (k % 2 == 0) res[resIdx++] = ((double)(find(root, k / 2 + 1)) + find(root, k / 2)) / 2;
            else res[resIdx++] = find(root, k / 2 + 1);
            delete(root, nums[i-k+1]);
        }
    
        return res; 
    }
    
    int find(TreeNode root, int idx) {
        if (root.cnt < idx && root.cnt + root.dup >= idx) return root.val;
        if (root.cnt >= idx) return find(root.left, idx);
        else return find(root.right, idx - root.dup - root.cnt);
    }
    
    TreeNode add(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (root.val == val) root.dup++;
        else if (root.val > val) {
            root.cnt++;
            root.left = add(root.left, val);
        } else {
            root.right = add(root.right, val);
        }
        return root;
    }
    
    void delete(TreeNode root, int val) {
        if (root.val == val) {
            root.dup--;
        } else if (root.val > val) {
            root.cnt--;
            delete(root.left, val);
        } else {
            delete(root.right, val);
        }
    }
}

class TreeNode {
    int val;
    int dup;
    int cnt;
    TreeNode left, right;
    TreeNode (int val) {
        this.val = val;
        dup = 1;
        cnt = 0;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/sliding-window-median/submissions/)***
