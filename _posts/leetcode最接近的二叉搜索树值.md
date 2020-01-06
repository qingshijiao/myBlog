---
title: 270.最接近的二叉搜索树值（Closest Binary Search Tree Value）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

270.Closest Binary Search Tree Value
Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**

- Given target value is a floating point.
- You are guaranteed to have only one unique value in the BST that is closest to the target.

Example:
```
Input: root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3

Output: 4
```

#### Solution1 - 迭代

Language: **Java**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int closestValue(TreeNode root, double target) {
        if (root == null) return 0;
        int min = root.val;
        while (root != null) {
            min = (Math.abs(root.val - target) < Math.abs(min - target) ? root.val : min);
            root = (root.val < target) ? root.right : root.left;
        }
        return min;
    }
}
```

#### Solution2 - 递归

Language: **Java**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int closestValue(TreeNode root, double target) {
        TreeNode child = target < root.val ? root.left : root.right;
        if (child == null) {
            return root.val;
        }
        int childClosest = closestValue(child, target);
        return Math.abs(root.val - target) < Math.abs(childClosest - target) ? root.val : childClosest;
    }
}
```

---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5025951.html)***
