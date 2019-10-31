---
title: 144.二叉树的前序遍历（Binary Tree Preorder Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，返回它的 前序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,2,3]
```
**进阶:**递归算法很简单，你可以通过迭代算法完成吗？



# 题解

## 官方题解
### 1.迭代
**思路：**

```
class Solution {
  public List<Integer> preorderTraversal(TreeNode root) {
    LinkedList<TreeNode> stack = new LinkedList<>();
    LinkedList<Integer> output = new LinkedList<>();
    if (root == null) {
      return output;
    }

    stack.add(root);
    while (!stack.isEmpty()) {
      TreeNode node = stack.pollLast();
      output.add(node.val);
      if (node.right != null) {
        stack.add(node.right);
      }
      if (node.left != null) {
        stack.add(node.left);
      }
    }
    return output;
  }
}

```
**复杂度分析：**
- 时间复杂度：访问每个节点恰好一次，时间复杂度为 O(N) ，其中 N 是节点的个数，也就是树的大小。
- 空间复杂度：取决于树的结构，最坏情况存储整棵树，因此空间复杂度是 O(N)。

### 2.莫里斯遍历
**思路：**
算法的思路是从当前节点向下访问先序遍历的前驱节点，每个前驱节点都恰好被访问两次。

首先从当前节点开始，向左孩子走一步然后沿着右孩子一直向下访问，直到到达一个叶子节点（当前节点的中序遍历前驱节点），所以我们更新输出并建立一条伪边 predecessor.right = root 更新这个前驱的下一个点。如果我们第二次访问到前驱节点，由于已经指向了当前节点，我们移除伪边并移动到下一个顶点。

如果第一步向左的移动不存在，就直接更新输出并向右移动。

![](https://pic.leetcode-cn.com/7ebbe8ee238e1faf5ec2e8bd263297660620eefaeaad3e63270efc98be80a4dc-image.png)
![](https://pic.leetcode-cn.com/61550b84f641c951d2930efd43aac9d425107c63bf0841c0ccf77c7f86a88541-image.png)
![](https://pic.leetcode-cn.com/b0d587de344a331d28f747d168ead3d66ce5bc19e607a4d269c586cbba7f0156-image.png)

```
class Solution {
  public List<Integer> preorderTraversal(TreeNode root) {
    LinkedList<Integer> output = new LinkedList<>();

    TreeNode node = root;
    while (node != null) {
      if (node.left == null) {
        output.add(node.val);
        node = node.right;
      }
      else {
        TreeNode predecessor = node.left;
        while ((predecessor.right != null) && (predecessor.right != node)) {
          predecessor = predecessor.right;
        }

        if (predecessor.right == null) {
          output.add(node.val);
          predecessor.right = node;
          node = node.left;
        }
        else{
          predecessor.right = null;
          node = node.right;
        }
      }
    }
    return output;
  }
}

```
**复杂度分析：**
- 时间复杂度：每个前驱恰好访问两次，因此复杂度是 O(N)，其中 NN 是顶点的个数，也就是树的大小。
- 空间复杂度：我们在计算中不需要额外空间，但是输出需要包含 N 个元素，因此空间复杂度为 O(N)。



## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/er-cha-shu-de-qian-xu-bian-li-by-leetcode/)***
