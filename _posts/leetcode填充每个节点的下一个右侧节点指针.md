---
title: 116.填充每个节点的下一个右侧节点指针（Populating Next Right Pointers in Each Node）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个完美二叉树，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

示例：
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/116_sample.png)

```
输入：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":null,"right":null,"val":4},"next":null,"right":{"$id":"4","left":null,"next":null,"right":null,"val":5},"val":2},"next":null,"right":{"$id":"5","left":{"$id":"6","left":null,"next":null,"right":null,"val":6},"next":null,"right":{"$id":"7","left":null,"next":null,"right":null,"val":7},"val":3},"val":1}

输出：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":{"$id":"4","left":null,"next":{"$id":"5","left":null,"next":{"$id":"6","left":null,"next":null,"right":null,"val":7},"right":null,"val":6},"right":null,"val":5},"right":null,"val":4},"next":{"$id":"7","left":{"$ref":"5"},"next":null,"right":{"$ref":"6"},"val":3},"right":{"$ref":"4"},"val":2},"next":null,"right":{"$ref":"7"},"val":1}

解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。

```

提示：

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

# 题解

## 官方题解
暂无


## 其他题解
### 1.递归
**思路：**

```
class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        if (root.left != null) {
            root.left.next = root.right;
            if (root.next != null) root.right.next = root.next.left;
        }
        connect(root.left);
        connect(root.right);
        return root;
    }
}


```


### 2.迭代
**思路：**

```
class Solution {
    public Node connect(Node root) {
        Node pre = root;
        while (pre != null) {
            Node cur = pre;
            while (cur != null) {
                if (cur.left != null) cur.left.next = cur.right;
                if (cur.right != null && cur.next != null) cur.right.next = cur.next.left;
                cur = cur.next;
            }
            pre = pre.left;
        }
        return root;
    }
}

```

### 3.BFS
**思路：**
```
public Node connect(Node root) {
    if (root == null) {
        return root;
    }
    Queue<Node> queue = new LinkedList<Node>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        Node pre = null;
        for (int i = 0; i < size; i++) {
            Node cur = queue.poll();
            //从第二个节点开始，将前一个节点的 pre 指向当前节点
            if (i > 0) {
                pre.next = cur;
            }
            pre = cur;
            if (cur.left != null) {
                queue.offer(cur.left);
            }
            if (cur.right != null) {
                queue.offer(cur.right);
            }

        }
    }
    return root;
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/submissions/)
[powcai](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/solution/di-gui-he-die-dai-by-powcai-4/)
[windliang](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--27/)***
