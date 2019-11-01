---
title: 145.二叉树的后序遍历（Binary Tree Postorder Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，返回它的 后序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [3,2,1]
```
**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？



# 题解

## 官方题解
### 1.迭代
**思路：**

```
class Solution {
  public List<Integer> postorderTraversal(TreeNode root) {
    LinkedList<TreeNode> stack = new LinkedList<>();
    LinkedList<Integer> output = new LinkedList<>();
    if (root == null) {
      return output;
    }

    stack.add(root);
    while (!stack.isEmpty()) {
      TreeNode node = stack.pollLast();
      output.addFirst(node.val);
      if (node.left != null) {
        stack.add(node.left);
      }
      if (node.right != null) {
        stack.add(node.right);
      }
    }
    return output;
  }
}

```
**复杂度分析：**
- 时间复杂度：访问每个节点恰好一次，因此时间复杂度为 O(N)，其中 N 是节点的个数，也就是树的大小。
- 空间复杂度：取决于树的结构，最坏情况需要保存整棵树，因此空间复杂度为 O(N)。

## 其他题解
### 1.递归
**思路：**
```
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    postorderTraversalHelper(root, list);
    return list;
}

private void postorderTraversalHelper(TreeNode root, List<Integer> list) {
    if (root == null) {
        return;
    }
    postorderTraversalHelper(root.left, list);
    postorderTraversalHelper(root.right, list);
    list.add(root.val);
}

```

### 2.栈
**思路：**
开始的话，也是不停的往左子树走，然后直到为 null 。不同之处是，之前直接把节点 pop 并且加入到 list 中，然后直接转到右子树。

这里的话，我们应该把节点 peek 出来，然后判断一下当前根节点的右子树是否为空或者是否是从右子树回到的根节点。

判断是否是从右子树回到的根节点，这里我用了一个 set ，当从左子树到根节点的时候，我把根节点加入到 set 中，之后我们就可以判断当前节点在不在 set 中，如果在的话就表明当前是第二次回来，也就意味着是从右子树到的根节点。

```
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    Set<TreeNode> set = new HashSet<>();
    TreeNode cur = root;
    while (cur != null || !stack.isEmpty()) {
        while (cur != null && !set.contains(cur)) {
            stack.push(cur);
            cur = cur.left;
        }
        cur = stack.peek();
        //右子树为空或者第二次来到这里
        if (cur.right == null || set.contains(cur)) {
            list.add(cur.val);
            set.add(cur);
            stack.pop();//将当前节点弹出
            if (stack.isEmpty()) {
                return list;
            }
            //转到右子树，这种情况对应于右子树为空的情况
            cur = stack.peek();
            cur = cur.right;
        //从左子树过来，加到 set 中，转到右子树
        } else {
            set.add(cur);
            cur = cur.right;
        }
    }
    return list;
}

```

上边的解法在判断当前是从左子树到的根节点还是右子树到的根节点用了 set ，这里 还有一个更直接的方法，通过记录上一次遍历的节点。

如果当前节点的右节点和上一次遍历的节点相同，那就表明当前是从右节点过来的了。

```
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode cur = root;
    TreeNode last = null;
    while (cur != null || !stack.isEmpty()) {
        if (cur != null) {
            stack.push(cur);
            cur = cur.left;
        } else {
            TreeNode temp = stack.peek();
            //是否变到右子树
            if (temp.right != null && temp.right != last) {
                cur = temp.right;
            } else {
                list.add(temp.val);
                last = temp;
                stack.pop();
            }
        }
    }
    return list;
}
```
我们还可以将左右子树分别压栈，然后每次从栈里取元素。需要注意的是，因为我们应该先访问左子树，而栈的话是先进后出，所以我们压栈先压右子树。
```
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    if (root == null) {
        return list;
    }
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode cur = stack.pop();
        if (cur == null) {
            continue;
        }
        if (!stack.isEmpty() && cur == stack.peek()) {
            stack.push(cur.right);
            stack.push(cur.right);
            stack.push(cur.left);
            stack.push(cur.left);
        } else {
            list.add(cur.val);
        }
    }
    return list;
}

```

## 3.转换问题
**思路：**
```
public List<Integer> postorderTraversal2(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode cur = root;
    while (cur != null || !stack.isEmpty()) {
        if (cur != null) {
            list.add(cur.val);
            stack.push(cur);
            cur = cur.right; // 考虑左子树
        } else {
            // 节点为空，就出栈
            cur = stack.pop();
            // 考虑右子树
            cur = cur.left;
        }
    }
    Collections.reverse(list);
    return list;
}

```

### 4.莫里斯遍历
**思路：**
所以总体思想就是：记当前遍历的节点为 cur。

- cur.left 为 null，保存 cur 的值，更新 cur = cur.right

- cur.left 不为 null，找到 cur.left 这颗子树最右边的节点记做 last

  - last.right 为 null，那么将 last.right = cur，更新 cur = cur.left

  - last.right 不为 null，说明之前已经访问过，第二次来到这里，表明当前子树遍历完成，保存 cur 的值，更新 cur = cur.right


![](https://pic.leetcode-cn.com/4db371d1014110e45e69c37b0b00d6fb37987e525f9929512194e9b916fdaac0.jpg)
![](https://pic.leetcode-cn.com/c4334635fef0244437d3c30e0a893467f455324131e398a1390c20a4cc218a99.jpg)
![](https://pic.leetcode-cn.com/aa8f05b33f7d8b409aad5e097d6593332d7144d66dbb4bc6db4fdf014c0373d9.jpg)



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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        TreeNode cur = root;
        while (cur != null) {
            // 情况 1
            if (cur.left == null) {
                cur = cur.right;
            } else {
                // 找左子树最右边的节点
                TreeNode pre = cur.left;
                while (pre.right != null && pre.right != cur) {
                    pre = pre.right;
                }
                // 情况 2.1
                if (pre.right == null) {
                    pre.right = cur;
                    cur = cur.left;
                }
                // 情况 2.2,第二次遍历节点
                if (pre.right == cur) {
                    pre.right = null; // 这里可以恢复为 null
                    //逆序
                    TreeNode head = reversList(cur.left);
                    //加入到 list 中，并且把逆序还原
                    reversList(head, list);
                    cur = cur.right;
                }
            }
        }
        TreeNode head = reversList(root);
        reversList(head, list);
        return list;
    }

    private TreeNode reversList(TreeNode head) {
        if (head == null) {
            return null;
        }
        TreeNode tail = head;
        head = head.right;

        tail.right = null;

        while (head != null) {
            TreeNode temp = head.right;
            head.right = tail;
            tail = head;
            head = temp;
        }

        return tail;
    }

    private TreeNode reversList(TreeNode head, List<Integer> list) {
        if (head == null) {
            return null;
        }
        TreeNode tail = head;
        head = head.right;
        list.add(tail.val);
        tail.right = null;

        while (head != null) {
            TreeNode temp = head.right;
            head.right = tail;
            tail = head;
            list.add(tail.val);
            head = temp;
        }
        return tail;
    }


}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/er-cha-shu-de-qian-xu-bian-li-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--34/)***
