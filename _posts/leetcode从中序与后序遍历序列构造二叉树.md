---
title: 106.从中序与后序遍历序列构造二叉树（Construct Binary Tree from Inorder and Postorder Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
根据一棵树的中序遍历与后序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出
```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```
返回如下的二叉树：
```
    3
   / \
  9  20
    /  \
   15   7
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.递归-范围
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
  public TreeNode buildTree(int[] inorder, int[] postorder) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < inorder.length; i++) {
        map.put(inorder[i], i);
    }
    return buildTreeHelper(inorder, 0, inorder.length, postorder, 0, postorder.length, map);
  }

  private TreeNode buildTreeHelper(int[] inorder, int i_start, int i_end, int[] postorder, int p_start, int p_end,
                                 HashMap<Integer, Integer> map) {
    if (p_start == p_end) {
        return null;
    }
    int root_val = postorder[p_end - 1];
    TreeNode root = new TreeNode(root_val);
    int i_root_index = map.get(root_val);
    int leftNum = i_root_index - i_start;
    root.left = buildTreeHelper(inorder, i_start, i_root_index, postorder, p_start, p_start + leftNum, map);
    root.right = buildTreeHelper(inorder, i_root_index + 1, i_end, postorder, p_start + leftNum, p_end - 1,
                                 map);
    return root;
  }
}
```

### 2.递归-stop
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
  int post;
  int in;
  public TreeNode buildTree(int[] inorder, int[] postorder) {
      post = postorder.length - 1;
      in = inorder.length - 1;
      return buildTreeHelper(inorder, postorder, (long) Integer.MIN_VALUE - 1);
  }

  private TreeNode buildTreeHelper(int[] inorder, int[] postorder, long stop) {
      if (post == -1) {
          return null;
      }
      if (inorder[in] == stop) {
          in--;
          return null;
      }
      int root_val = postorder[post--];
      TreeNode root = new TreeNode(root_val);
      root.right = buildTreeHelper(inorder, postorder, root_val);
      root.left = buildTreeHelper(inorder, postorder, stop);
      return root;
  }
}
```

### 3.迭代 栈
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
  public TreeNode buildTree(int[] inorder, int[] postorder) {
    if (postorder.length == 0) {
        return null;
    }
    Stack<TreeNode> roots = new Stack<TreeNode>();
    int post = postorder.length - 1;
    int in = inorder.length - 1;
    TreeNode curRoot = new TreeNode(postorder[post]);
    TreeNode root = curRoot;
    roots.push(curRoot);
    post--;
    while (post >=  0) {
        if (curRoot.val == inorder[in]) {
            while (!roots.isEmpty() && roots.peek().val == inorder[in]) {
                curRoot = roots.peek();
                roots.pop();
                in--;
            }
            curRoot.left = new TreeNode(postorder[post]);
            curRoot = curRoot.left;
            roots.push(curRoot);
            post--;
        } else {
            curRoot.right = new TreeNode(postorder[post]);
            curRoot = curRoot.right;
            roots.push(curRoot);
            post--;
        }
    }
    return root;
  }


}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/submissions/)
[windliang](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-23/)***
