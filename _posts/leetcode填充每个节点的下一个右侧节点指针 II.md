---
title: 117.填充每个节点的下一个右侧节点指针 II（Populating Next Right Pointers in Each Node II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树
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
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png)

```
输入：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":null,"right":null,"val":4},"next":null,"right":{"$id":"4","left":null,"next":null,"right":null,"val":5},"val":2},"next":null,"right":{"$id":"5","left":null,"next":null,"right":{"$id":"6","left":null,"next":null,"right":null,"val":7},"val":3},"val":1}

输出：{"$id":"1","left":{"$id":"2","left":{"$id":"3","left":null,"next":{"$id":"4","left":null,"next":{"$id":"5","left":null,"next":null,"right":null,"val":7},"right":null,"val":5},"right":null,"val":4},"next":{"$id":"6","left":null,"next":null,"right":{"$ref":"5"},"val":3},"right":{"$ref":"4"},"val":2},"next":null,"right":{"$ref":"6"},"val":1}

解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。

```

提示：

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

# 题解

## 官方题解
暂无


## 其他题解
### 1.BFS
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


### 2.迭代
**思路：**

```
Node connect(Node root) {
    if (root == null)
        return root;
    Node pre = root;
    Node cur = null;
    while (true) {
        cur = pre;
        while (cur != null) {
            //找到至少有一个孩子的节点
            if (cur.left == null && cur.right == null) {
                cur = cur.next;
                continue;
            }
            //找到当前节点的下一个至少有一个孩子的节点
            Node next = cur.next;
            while (next != null && next.left == null && next.right == null) {
                next = next.next;
                if (next == null) {
                    break;
                }
            }
            //当前节点的左右孩子都不为空，就将 left.next 指向 right
            if (cur.left != null && cur.right != null) {
                cur.left.next = cur.right;
            }
            //要接上 next 的节点的孩子，所以用 temp 处理当前节点 right 为 null 的情况
            Node temp = cur.right == null ? cur.left : cur.right;

            if (next != null) {
                //next 左孩子不为 null，就接上左孩子。
                if (next.left != null) {
                    temp.next = next.left;
                //next 左孩子为 null，就接上右孩子。
                } else {
                    temp.next = next.right;
                }
            }

            cur = cur.next;
        }
        //找到拥有孩子的节点
        while (pre.left == null && pre.right == null) {
            pre = pre.next;
            //都没有孩子说明已经是最后一层了
            if (pre == null) {
                return root;
            }
        }
        //进入下一层
        pre = pre.left != null ? pre.left : pre.right;
    }
}
```

### 3.哑节点
**思路：**
![](https://pic.leetcode-cn.com/0dc6ed6ba29a12469f6254b1016c90608b852131939d03fd23d4bbd1aa0a9d78.jpg)

```
Node connect(Node root) {
    Node cur = root;
    while (cur != null) {
        Node dummy = new Node();
        Node tail = dummy;
        //遍历 cur 的当前层
        while (cur != null) {
            if (cur.left != null) {
                tail.next = cur.left;
                tail = tail.next;
            }
            if (cur.right != null) {
                tail.next = cur.right;
                tail = tail.next;
            }
            cur = cur.next;
        }
        //更新 cur 到下一层
        cur = dummy.next;
    }
    return root;
}

```




---
***参考：
[LeetCode](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/submissions/)
[windliang](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-28/)***
