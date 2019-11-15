---
title: 173.二叉搜索树迭代器（Binary Search Tree Iterator）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
实现一个二叉搜索树迭代器。你将使用二叉搜索树的根节点初始化迭代器。

调用 next() 将返回二叉搜索树中的下一个最小的数。



示例：
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/25/bst-tree.png)

```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // 返回 3
iterator.next();    // 返回 7
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 9
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 15
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 20
iterator.hasNext(); // 返回 false
```

**提示：**

- next() 和 hasNext() 操作的时间复杂度是 O(1)，并使用 O(h) 内存，其中 h 是树的高度。
- 你可以假设 next() 调用总是有效的，也就是说，当调用 next() 时，BST 中至少存在一个下一个最小的数。


# 题解

## 官方题解
暂无

## 其他题解
### 1.栈
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
class BSTIterator {
    // 中序遍历
    private Stack<TreeNode> stack = new Stack<>();
    private TreeNode curr;

    public BSTIterator(TreeNode root) {
        curr = root;
    }

    /** @return the next smallest number */
    public int next() {
        // 所有子节点进栈
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        // 第一个出栈的节点为最左节点，即为最小值
        TreeNode ans = stack.pop();
        // 开始遍历右子节点
        curr = ans.right;
        return ans.val;
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty() || curr != null;
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

### 2.链表 - 中序遍历
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
class BSTIterator {

    public BSTIterator(TreeNode root) {
        midOrder(root);
    }

    /** @return the next smallest number */
    public int next() {
        if(list != null && list.size() > index){
            return list.get(index++).val;
        }else{
            return -1;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return (list != null && list.size() > index);
    }

    private int index = 0;
    private List<TreeNode> list = new ArrayList<>();
    private void midOrder(TreeNode root){
        if(root != null){
            midOrder(root.left);
            list.add(root);
            midOrder(root.right);
        }
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-search-tree-iterator/submissions/)
[voiddme](https://leetcode-cn.com/problems/binary-search-tree-iterator/solution/zhong-xu-bian-li-java-by-voiddme/)***
