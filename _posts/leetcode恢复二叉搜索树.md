---
title: 99.恢复二叉搜索树（Recover Binary Search Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
二叉搜索树中的两个节点被错误地交换。

请在不改变其结构的情况下，恢复这棵树。

示例 1:
```
输入: [1,3,null,null,2]

   1
  /
 3
  \
   2

输出: [3,1,null,null,2]

   3
  /
 1
  \
   2
```

示例 2:
```
输入: [3,1,4,null,null,2]

  3
 / \
1   4
   /
  2

输出: [2,1,4,null,null,3]

  2
 / \
1   4
   /
  3
```
**进阶:**

使用 O(n) 空间复杂度的解法很容易实现。
你能想出一个只使用常数空间的解决方案吗？


# 题解

## 官方题解
暂无

## 其他题解
### 1.中序遍历的递归
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
    TreeNode first = null;
    TreeNode second = null;
    TreeNode pre = null;

    public void recoverTree(TreeNode root) {
        inorderTraversal(root);
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }

    public void inorderTraversal(TreeNode root) {
        if (root == null)
            return;
        inorderTraversal(root.left);
        if (pre != null) {
            if (first == null && pre.val > root.val)
                first = pre;
            if (first != null && pre.val > root.val)
                second = root;
        }
        pre = root;
        inorderTraversal(root.right);
    }
}

```

### 2.栈
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
    TreeNode first = null;
    TreeNode second = null;

    public void recoverTree(TreeNode root) {
        inorderTraversal(root);
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }

    public void inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode pre = null;
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            if (pre != null) {
                if (first == null && pre.val > root.val)
                    first = pre;
                if (first != null && pre.val > root.val)
                    second = root;
            }
            pre = root;
            root = root.right;
        }
    }

}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/recover-binary-search-tree/submissions/)
[spirit-9](https://leetcode-cn.com/problems/recover-binary-search-tree/solution/java-yi-dong-yi-jie-xiao-lu-gao-by-spirit-9-55/)***
