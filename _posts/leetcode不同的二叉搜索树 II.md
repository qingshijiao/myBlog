---
title: 95.不同的二叉搜索树 II（Unique Binary Search Trees II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。

示例:
```
输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```



# 题解

## 官方题解
### 1.递归
**思路：**
我们从序列 1 ..n 中取出数字 i，作为当前树的树根。于是，剩余 i - 1 个元素可用于左子树，n - i 个元素用于右子树。这样会产生 G(i - 1) 种左子树 和 G(n - i) 种右子树，其中 G 是卡特兰数。

![](https://pic.leetcode-cn.com/f709dff506c20ac970d4cd7ace0436aafca7828c67b510cdbaaa60d54f5479b3-image.png)

现在，我们对序列 1 ... i - 1 重复上述过程，以构建所有的左子树；然后对 i + 1 ... n 重复，以构建所有的右子树。

这样，我们就有了树根 i 和可能的左子树、右子树的列表。

最后一步，对两个列表循环，将左子树和右子树连接在根上。


```
class Solution {
  public LinkedList<TreeNode> generate_trees(int start, int end) {
    LinkedList<TreeNode> all_trees = new LinkedList<TreeNode>();
    if (start > end) {
      all_trees.add(null);
      return all_trees;
    }

    // pick up a root
    for (int i = start; i <= end; i++) {
      // all possible left subtrees if i is choosen to be a root
      LinkedList<TreeNode> left_trees = generate_trees(start, i - 1);

      // all possible right subtrees if i is choosen to be a root
      LinkedList<TreeNode> right_trees = generate_trees(i + 1, end);

      // connect left and right trees to the root i
      for (TreeNode l : left_trees) {
        for (TreeNode r : right_trees) {
          TreeNode current_tree = new TreeNode(i);
          current_tree.left = l;
          current_tree.right = r;
          all_trees.add(current_tree);
        }
      }
    }
    return all_trees;
  }

  public List<TreeNode> generateTrees(int n) {
    if (n == 0) {
      return new LinkedList<TreeNode>();
    }
    return generate_trees(1, n);
  }
}


```
![](https://i.loli.net/2019/10/07/5usPLcYoFJ8mylI.png)



## 其他题解
### 1.回溯
**思路：**

```

```

### 2.动态规划-自底而上
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
    public List<TreeNode> generateTrees(int n) {
        ArrayList<TreeNode>[] dp = new ArrayList[n + 1];
        dp[0] = new ArrayList<TreeNode>();
        if (n == 0) {
            return dp[0];
        }
        dp[0].add(null);
        //长度为 1 到 n
        for (int len = 1; len <= n; len++) {
            dp[len] = new ArrayList<TreeNode>();
            //将不同的数字作为根节点，只需要考虑到 len
            for (int root = 1; root <= len; root++) {
                int left = root - 1;  //左子树的长度
                int right = len - root; //右子树的长度
                for (TreeNode leftTree : dp[left]) {
                    for (TreeNode rightTree : dp[right]) {
                        TreeNode treeRoot = new TreeNode(root);
                        treeRoot.left = leftTree;
                        //克隆右子树并且加上偏差
                        treeRoot.right = clone(rightTree, root);
                        dp[len].add(treeRoot);
                    }
                }
            }
        }
        return dp[n];
    }

    private TreeNode clone(TreeNode n, int offset) {
        if (n == null) {
            return null;
        }
        TreeNode node = new TreeNode(n.val + offset);
        node.left = clone(n.left, offset);
        node.right = clone(n.right, offset);
        return node;
    }

}
```

### 3.动态规划
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
  public List<TreeNode> generateTrees(int n) {
    List<TreeNode> pre = new ArrayList<TreeNode>();
    if (n == 0) {
        return pre;
    }
    pre.add(null);
    //每次增加一个数字
    for (int i = 1; i <= n; i++) {
        List<TreeNode> cur = new ArrayList<TreeNode>();
        //遍历之前的所有解
        for (TreeNode root : pre) {
            //插入到根节点
            TreeNode insert = new TreeNode(i);
            insert.left = root;
            cur.add(insert);
            //插入到右孩子，右孩子的右孩子...最多找 n 次孩子
            for (int j = 0; j <= n; j++) {
                TreeNode root_copy = treeCopy(root); //复制当前的树
                TreeNode right = root_copy; //找到要插入右孩子的位置
                int k = 0;
                //遍历 j 次找右孩子
                for (; k < j; k++) {
                    if (right == null)
                        break;
                    right = right.right;
                }
                //到达 null 提前结束
                if (right == null)
                    break;
                //保存当前右孩子的位置的子树作为插入节点的左孩子
                TreeNode rightTree = right.right;
                insert = new TreeNode(i);
                right.right = insert; //右孩子是插入的节点
                insert.left = rightTree; //插入节点的左孩子更新为插入位置之前的子树
                //加入结果中
                cur.add(root_copy);
            }
        }
        pre = cur;

    }
    return pre;
  }


  private TreeNode treeCopy(TreeNode root) {
    if (root == null) {
        return root;
    }
    TreeNode newRoot = new TreeNode(root.val);
    newRoot.left = treeCopy(root.left);
    newRoot.right = treeCopy(root.right);
    return newRoot;
  }


}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/bu-tong-de-er-cha-sou-suo-shu-ii-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-2-7/)***
