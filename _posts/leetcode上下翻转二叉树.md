---
title: 156.上下翻转二叉树（Binary Tree Upside Down）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
Given a binary tree where all the right nodes are either leaf nodes with a sibling (a left node that shares the same parent node) or empty, flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

Example:

Input: [1,2,3,4,5]
```
    1
   / \
  2   3
 / \
4   5
```
Output: return the root of the binary tree [4,5,2,#,#,3,1]
```
   4
  / \
 5   2
    / \
   3   1
```
Clarification:

Confused what [4,5,2,#,#,3,1] means? Read more below on how binary tree is serialized on OJ.

The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.

Here's an example:
```
   1
  / \
 2   3
    /
   4
    \
     5
```
The above binary tree is serialized as [1,2,3,#,#,4,#,#,5].


# 题解

## 官方题解
暂无

## 其他题解
### 1.递归
**思路：** 上下颠倒后原来二叉树的最左子节点变成了根节点，其对应的右节点变成了其左子节点，其父节点变成了其右子节点，相当于顺时针旋转了一下。


```
// Recursion
class Solution {
public:
    TreeNode *upsideDownBinaryTree(TreeNode *root) {
        if (!root || !root->left) return root;
        TreeNode *l = root->left, *r = root->right;
        TreeNode *res = upsideDownBinaryTree(l);
        l->left = r;
        l->right = root;
        root->left = NULL;
        root->right = NULL;
        return res;
    }
};

```

### 2.迭代
**思路：**
```
// Iterative
class Solution {
public:
    TreeNode *upsideDownBinaryTree(TreeNode *root) {
        TreeNode *cur = root, *pre = NULL, *next = NULL, *tmp = NULL;
        while (cur) {
            next = cur->left;
            cur->left = tmp;
            tmp = cur->right;
            cur->right = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/5172838.html)***
