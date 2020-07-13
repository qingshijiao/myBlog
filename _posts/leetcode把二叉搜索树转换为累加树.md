---
title: 538. 把二叉搜索树转换为累加树 (Convert BST to Greater Tree)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [538\. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

Difficulty: **简单**


给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

**例如：**

```
输入: 原始二叉搜索树:
              5
            /   \
           2     13

输出: 转换为累加树:
             18
            /   \
          20     13
```

**注意：**本题和 1038:  相同


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
    int sum=0;
    public TreeNode convertBST(TreeNode root) {
        if(root==null)
            return null;
        else{
            convertBST(root.right);
            sum+=root.val;
            root.val=sum;
            convertBST(root.left);
        }
        return root;
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)***
