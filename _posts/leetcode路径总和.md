---
title: 112.路径总和（Path Sum）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

示例: 
给定如下二叉树，以及目标和 sum = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```
返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。


# 题解

## 官方题解
### 1.递归
**思路：**


```
class Solution {
  public boolean hasPathSum(TreeNode root, int sum) {
    if (root == null)
      return false;

    sum -= root.val;
    if ((root.left == null) && (root.right == null))
      return (sum == 0);
    return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
  }
}

```
**复杂度分析：**
- 时间复杂度：我们访问每个节点一次，时间复杂度为 O(N) ，其中 N 是节点个数。
- 空间复杂度：最坏情况下，整棵树是非平衡的，例如每个节点都只有一个孩子，递归会调用 N （树的高度）次，因此栈的空间开销是 O(N) 。但在最好情况下，树是完全平衡的，高度只有 log(N)，因此在这种情况下空间复杂度只有 O(log(N)) 。



### 2.迭代
**思路：**


```
class Solution {
  public boolean hasPathSum(TreeNode root, int sum) {
    if (root == null)
      return false;

    LinkedList<TreeNode> node_stack = new LinkedList();
    LinkedList<Integer> sum_stack = new LinkedList();
    node_stack.add(root);
    sum_stack.add(sum - root.val);

    TreeNode node;
    int curr_sum;
    while ( !node_stack.isEmpty() ) {
      node = node_stack.pollLast();
      curr_sum = sum_stack.pollLast();
      if ((node.right == null) && (node.left == null) && (curr_sum == 0))
        return true;

      if (node.right != null) {
        node_stack.add(node.right);
        sum_stack.add(curr_sum - node.right.val);
      }
      if (node.left != null) {
        node_stack.add(node.left);
        sum_stack.add(curr_sum - node.left.val);
      }
    }
    return false;
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N)。
- 空间复杂度：当树不平衡的最坏情况下是 O(N) 。在最好情况（树是平衡的）下是 O(logN)。


## 其他题解

### 1.BFS
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
    public boolean hasPathSum(TreeNode root, int sum) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        Queue<Integer> queueSum = new LinkedList<Integer>();
        if (root == null)
            return false;
        queue.offer(root);
        queueSum.offer(root.val);
        while (!queue.isEmpty()) {
            int levelNum = queue.size(); // 当前层元素的个数
            for (int i = 0; i < levelNum; i++) {
                TreeNode curNode = queue.poll();
                int curSum = queueSum.poll();
                if (curNode != null) {
                    //判断叶子节点是否满足了条件
                    if (curNode.left == null && curNode.right == null && curSum == sum) {
                        return true;
                    }
                    //当前节点和累计的和加入队列
                    if (curNode.left != null) {
                        queue.offer(curNode.left);
                        queueSum.offer(curSum + curNode.left.val);
                    }
                    if (curNode.right != null) {
                        queue.offer(curNode.right);
                        queueSum.offer(curSum + curNode.right.val);
                    }
                }
            }
        }
        return false;
    }
}
```

### 2.DFS
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
    public boolean hasPathSum(TreeNode root, int sum) {
        List<Integer> result = new LinkedList<>();
        Stack<TreeNode> toVisit = new Stack<>();
        TreeNode cur = root;
        TreeNode pre = null;
        int curSum = 0; //记录当前的累计的和
        while (cur != null || !toVisit.isEmpty()) {
            while (cur != null) {
                toVisit.push(cur); // 添加根节点
                curSum += cur.val;
                cur = cur.left; // 递归添加左节点
            }
            cur = toVisit.peek(); // 已经访问到最左的节点了
            //判断是否满足条件
            if (curSum == sum && cur.left == null && cur.right == null) {
                return true;
            }
            // 在不存在右节点或者右节点已经访问过的情况下，访问根节点
            if (cur.right == null || cur.right == pre) {
                TreeNode pop = toVisit.pop();
                curSum -= pop.val; //减去出栈的值
                pre = cur;
                cur = null;
            } else {
                cur = cur.right; // 右节点还没有访问过就先访问右节点
            }
        }
        return false;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/path-sum/solution/lu-jing-zong-he-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/path-sum/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-26/)***
