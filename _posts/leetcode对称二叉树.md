---
title: 101.对称二叉树（Symmetric Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
**说明:**

如果你可以运用递归和迭代两种方法解决这个问题，会很加分。



# 题解

## 官方题解
### 1.递归
**思路：**
![](https://pic.leetcode-cn.com/2c9a13df75821ba472de5267470481e48386ffa658b3f91a8acca5abfa43625d-file_1555698500306)

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
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root, root);
    }

    public boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return true;
        if (t1 == null || t2 == null) return false;
        return (t1.val == t2.val)
            && isMirror(t1.right, t2.left)
            && isMirror(t1.left, t2.right);
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)，因为我们遍历整个输入树一次，所以总的运行时间为 O(n)，其中 nn 是树中结点的总数。
- 空间复杂度：递归调用的次数受树的高度限制。在最糟糕情况下，树是线性的，其高度为 O(n)O(n)。因此，在最糟糕的情况下，由栈上的递归调用造成的空间复杂度为 O(n)。



### 2.迭代
**思路：**
除了递归的方法外，我们也可以利用队列进行迭代。队列中每两个连续的结点应该是相等的，而且它们的子树互为镜像。最初，队列中包含的是 root 以及 root。该算法的工作原理类似于 BFS，但存在一些关键差异。每次提取两个结点并比较它们的值。然后，将两个结点的左右子结点按相反的顺序插入队列中。当队列为空时，或者我们检测到树不对称（即从队列中取出两个不相等的连续结点）时，该算法结束。


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
  public boolean isSymmetric(TreeNode root) {
    Queue<TreeNode> q = new LinkedList<>();
    q.add(root);
    q.add(root);
    while (!q.isEmpty()) {
        TreeNode t1 = q.poll();
        TreeNode t2 = q.poll();
        if (t1 == null && t2 == null) continue;
        if (t1 == null || t2 == null) return false;
        if (t1.val != t2.val) return false;
        q.add(t1.left);
        q.add(t2.right);
        q.add(t1.right);
        q.add(t2.left);
    }
    return true;
  }

}
```
**复杂度分析：**
- 时间复杂度：O(n)，因为我们遍历整个输入树一次，所以总的运行时间为 O(n)，其中 nn 是树中结点的总数。
- 空间复杂度：递归调用的次数受树的高度限制。在最糟糕情况下，树是线性的，其高度为 O(n)O(n)。因此，在最糟糕的情况下，由栈上的递归调用造成的空间复杂度为 O(n)。

## 其他题解
### 1.DFS
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
  public boolean isSymmetric(TreeNode root) {
    if (root == null) {
        return true;
    }
    Stack<TreeNode> stackLeft = new Stack<>();
    Stack<TreeNode> stackRight = new Stack<>();
    TreeNode curLeft = root.left;
    TreeNode curRight = root.right;
    while (curLeft != null || !stackLeft.isEmpty() || curRight!=null || !stackRight.isEmpty()) {
        // 节点不为空一直压栈
        while (curLeft != null) {
            stackLeft.push(curLeft);
            curLeft = curLeft.left; // 考虑左子树
        }
        while (curRight != null) {
            stackRight.push(curRight);
            curRight = curRight.right; // 考虑右子树
        }
        //长度不同就返回 false
        if (stackLeft.size() != stackRight.size()) {
            return false;
        }
        // 节点为空，就出栈
        curLeft = stackLeft.pop();
        curRight = stackRight.pop();

        // 当前值判断
        if (curLeft.val != curRight.val) {
            return false;
        }
        // 考虑右子树
        curLeft = curLeft.right;
        curRight = curRight.left;
    }
    return true;
}


}
```

### 2.BFS
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
  public boolean isSymmetric6(TreeNode root) {
    if (root == null) {
        return true;
    }
    Queue<TreeNode> leftTree = new LinkedList<>();
    Queue<TreeNode> rightTree = new LinkedList<>();
    //两个树的根节点分别加入
    leftTree.offer(root.left);
    rightTree.offer(root.right);
    while (!leftTree.isEmpty() && !rightTree.isEmpty()) {
        TreeNode curLeft = leftTree.poll();
        TreeNode curRight = rightTree.poll();
        if (curLeft == null && curRight != null || curLeft != null && curRight == null) {
            return false;
        }
        if (curLeft != null && curRight != null) {
            if (curLeft.val != curRight.val) {
                return false;
            }
            //先加入左子树后加入右子树
            leftTree.offer(curLeft.left);
            leftTree.offer(curLeft.right);

            //先加入右子树后加入左子树
            rightTree.offer(curRight.right);
            rightTree.offer(curRight.left);
        }

    }
    if (!leftTree.isEmpty() || !rightTree.isEmpty()) {
        return false;
    }
    return true;
}


}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/symmetric-tree/solution/dui-cheng-er-cha-shu-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/symmetric-tree/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--21/)***
