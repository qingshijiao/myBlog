---
title: 129. 求根到叶子节点数字之和（Sum Root to Leaf Numbers）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 1->2->3 代表数字 123。

计算从根到叶子节点生成的所有数字之和。

**说明:** 叶子节点是指没有子节点的节点。

示例 1:
```
输入: [1,2,3]
    1
   / \
  2   3
输出: 25
解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.
```
示例 2:
```
输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026
解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
```



# 题解

## 官方题解
暂无

## 其他题解
### 1.回溯法
**思路：**
回溯的思想就是一直进行深度遍历，直到得到一个解后，记录当前解。然后再回到之前的状态继续进行深度遍历。

```
public int sumNumbers(TreeNode root) {
    if (root == null) {
        return 0;
    }
    dfs(root, root.val);
    return sum;
}

int sum = 0;

private void dfs(TreeNode root, int cursum) {
    //到达叶子节点
    if (root.left == null && root.right == null) {
        sum += cursum;
        return;
    }
    //尝试左子树
    if(root.left!=null){
        dfs(root.left,  cursum * 10 + root.left.val);
    }
    //尝试右子树
    if(root.right!=null){
        dfs(root.right, cursum * 10 + root.right.val);

    }

}
```

### 2.分治法
**思路：**
分支法的思想就是，解决子问题，通过子问题解决最终问题。

要求一个树所有的路径和，我们只需要知道从根节点出发经过左子树的所有路径和和从根节点出发经过右子树的所有路径和，加起来就可以了。



```
public int sumNumbers(TreeNode root) {
    if (root == null) {
        return 0;
    }
    return sumNumbersHelper(root, 0);
}

private int sumNumbersHelper(TreeNode root, int sum) {
    //已经累计的和
    int cursum = sum * 10 + root.val;
    if (root.left == null && root.right == null) {
        return cursum;
    }
    int ans = 0;
    //从最开始经过当前 root 再经过左孩子到达叶子节点所有的路径和
    if (root.left != null) {
        ans += sumNumbersHelper(root.left, cursum);
    }
    //从最开始经过当前 root 再经过右孩子到达叶子节点所有的路径和
    if (root.right != null) {
        ans += sumNumbersHelper(root.right, cursum);
    }
    //返回从最开始经过当前 root 然后到达叶子节点所有的路径和
    return ans;
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/submissions/)
[windliang](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-5/)***
