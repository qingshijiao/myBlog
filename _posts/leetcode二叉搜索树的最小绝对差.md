---
title: 530. 二叉搜索树的最小绝对差（Minimum Absolute Difference in BST）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [530\. Minimum Absolute Difference in BST](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

Difficulty: **简单**


给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。

**示例：**

```
输入：

   1
    \
     3
    /
   2

输出：
1

解释：
最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。
```

**提示：**

*   树中至少有 2 个节点。
*   本题与 783 相同


#### Solution

Language: **Java**

```java
​/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    TreeNode pre = null;
    int min = Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        pre(root);
        return min;
    }
    public void pre(TreeNode root){
        if(root == null){
            return;
        }
        pre(root.left);
        if(pre != null){
            min = Math.min(min,root.val-pre.val);
        }
        pre = root;
        pre(root.right);

    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)***
