---
title: 105.从前序与中序遍历序列构造二叉树（Construct Binary Tree from Preorder and Inorder Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
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
### 1.递归
**思路：**
![](https://pic.leetcode-cn.com/500854d776e58340f39ffe7641bad58d747122e28ed8ce816ec36e6b518987e0-image.png)
![](https://pic.leetcode-cn.com/f839b10def0240ed3efb46deaa6fb2222073588beb56cffaf4c9d09d8b2dafb0-image.png)

```
class Solution {
  // start from first preorder element
  int pre_idx = 0;
  int[] preorder;
  int[] inorder;
  HashMap<Integer, Integer> idx_map = new HashMap<Integer, Integer>();

  public TreeNode helper(int in_left, int in_right) {
    // if there is no elements to construct subtrees
    if (in_left == in_right)
      return null;

    // pick up pre_idx element as a root
    int root_val = preorder[pre_idx];
    TreeNode root = new TreeNode(root_val);

    // root splits inorder list
    // into left and right subtrees
    int index = idx_map.get(root_val);

    // recursion
    pre_idx++;
    // build left subtree
    root.left = helper(in_left, index);
    // build right subtree
    root.right = helper(index + 1, in_right);
    return root;
  }

  public TreeNode buildTree(int[] preorder, int[] inorder) {
    this.preorder = preorder;
    this.inorder = inorder;

    // build a hashmap value -> its index
    int idx = 0;
    for (Integer val : inorder)
      idx_map.put(val, idx++);
    return helper(0, inorder.length);
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N)。
- 空间复杂度：O(N)，存储整棵树的开销。

## 其他题解
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTreeHelper(preorder,  inorder, (long)Integer.MAX_VALUE + 1);
    }
    int pre = 0;
    int in = 0;
    private TreeNode buildTreeHelper(int[] preorder, int[] inorder, long stop) {
        //到达末尾返回 null
        if(pre == preorder.length){
            return null;
        }
        //到达停止点返回 null
        //当前停止点已经用了，in 后移
        if (inorder[in] == stop) {
            in++;
            return null;
        }
        int root_val = preorder[pre++];
        TreeNode root = new TreeNode(root_val);
        //左子树的停止点是当前的根节点
        root.left = buildTreeHelper(preorder,  inorder, root_val);
        //右子树的停止点是当前树的停止点
        root.right = buildTreeHelper(preorder, inorder, stop);
        return root;
    }
}
```

### 2.迭代 栈
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
  public TreeNode buildTree(int[] preorder, int[] inorder) {
    if (preorder.length == 0) {
        return null;
    }
    Stack<TreeNode> roots = new Stack<TreeNode>();
    int pre = 0;
    int in = 0;
    //先序遍历第一个值作为根节点
    TreeNode curRoot = new TreeNode(preorder[pre]);
    TreeNode root = curRoot;
    roots.push(curRoot);
    pre++;
    //遍历前序遍历的数组
    while (pre < preorder.length) {
        //出现了当前节点的值和中序遍历数组的值相等，寻找是谁的右子树
        if (curRoot.val == inorder[in]) {
            //每次进行出栈，实现倒着遍历
            while (!roots.isEmpty() && roots.peek().val == inorder[in]) {
                curRoot = roots.peek();
                roots.pop();
                in++;
            }
            //设为当前的右孩子
            curRoot.right = new TreeNode(preorder[pre]);
            //更新 curRoot
            curRoot = curRoot.right;
            roots.push(curRoot);
            pre++;
        } else {
            //否则的话就一直作为左子树
            curRoot.left = new TreeNode(preorder[pre]);
            curRoot = curRoot.left;
            roots.push(curRoot);
            pre++;
        }
    }
    return root;
  }

}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/solution/cong-qian-xu-he-zhong-xu-bian-li-xu-lie-gou-zao-er/)
[windliang](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--22/)***
