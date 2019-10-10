---
title: 102.二叉树的层次遍历（Binary Tree Level Order Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回其层次遍历结果：
```
[
  [3],
  [9,20],
  [15,7]
]
```


# 题解

## 官方题解
### 1.递归
**思路：**

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
 class Solution {
     List<List<Integer>> levels = new ArrayList<List<Integer>>();

     public void helper(TreeNode node, int level) {
         // start the current level
         if (levels.size() == level)
             levels.add(new ArrayList<Integer>());

          // fulfil the current level
          levels.get(level).add(node.val);

          // process child nodes for the next level
          if (node.left != null)
             helper(node.left, level + 1);
          if (node.right != null)
             helper(node.right, level + 1);
     }

     public List<List<Integer>> levelOrder(TreeNode root) {
         if (root == null) return levels;
         helper(root, 0);
         return levels;
     }
 }


```
**复杂度分析：**
- 时间复杂度：O(N)，因为每个节点恰好会被运算一次。
- 空间复杂度：O(N)，保存输出结果的数组包含 N 个节点的值。



### 2.迭代
**思路：**

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
 public List<List<Integer>> levelOrder(TreeNode root) {
   List<List<Integer>> levels = new ArrayList<List<Integer>>();
   if (root == null) return levels;

   Queue<TreeNode> queue = new LinkedList<TreeNode>();
   queue.add(root);
   int level = 0;
   while ( !queue.isEmpty() ) {
     // start the current level
     levels.add(new ArrayList<Integer>());

     // number of elements in the current level
     int level_length = queue.size();
     for(int i = 0; i < level_length; ++i) {
       TreeNode node = queue.remove();

       // fulfill the current level
       levels.get(level).add(node.val);

       // add child nodes of the current level
       // in the queue for the next level
       if (node.left != null) queue.add(node.left);
       if (node.right != null) queue.add(node.right);
     }
     // go to next level
     level++;
   }
   return levels;
 }
}
```
**复杂度分析：**
- 时间复杂度：O(N)，因为每个节点恰好会被运算一次。
- 空间复杂度：O(N)，保存输出结果的数组包含 N 个节点的值。

## 其他题解
暂无



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/solution/er-cha-shu-de-ceng-ci-bian-li-by-leetcode/)***
