---
title: 138.复制带随机指针的链表（Copy List with Random Pointer）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。

要求返回这个链表的深拷贝。 

 

示例：

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/23/1470150906153-2yxeznm.png)

```
输入：
{"$id":"1","next":{"$id":"2","next":null,"random":{"$ref":"2"},"val":2},"random":{"$ref":"2"},"val":1}

解释：
节点 1 的值是 1，它的下一个指针和随机指针都指向节点 2 。
节点 2 的值是 2，它的下一个指针指向 null，随机指针指向它自己。
```

**提示：**

你必须返回给定头的拷贝作为对克隆列表的引用。



# 题解

## 官方题解
### 1.回溯
**思路：**
![](https://pic.leetcode-cn.com/bd3fb0c9f6d3fdcc3bbc4afdb47183d6aaef93552df135130ea42da77aab911d-image.png)

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
public class Solution {
  // HashMap which holds old nodes as keys and new nodes as its values.
  HashMap<Node, Node> visitedHash = new HashMap<Node, Node>();

  public Node copyRandomList(Node head) {

    if (head == null) {
      return null;
    }

    // If we have already processed the current node, then we simply return the cloned version of
    // it.
    if (this.visitedHash.containsKey(head)) {
      return this.visitedHash.get(head);
    }

    // Create a new node with the value same as old node. (i.e. copy the node)
    Node node = new Node(head.val, null, null);

    // Save this value in the hash map. This is needed since there might be
    // loops during traversal due to randomness of random pointers and this would help us avoid
    // them.
    this.visitedHash.put(head, node);

    // Recursively copy the remaining linked list starting once from the next pointer and then from
    // the random pointer.
    // Thus we have two independent recursive calls.
    // Finally we update the next and random pointers for the new node created.
    node.next = this.copyRandomList(head.next);
    node.random = this.copyRandomList(head.random);

    return node;
  }
}
```
**复杂度分析：**
- 时间复杂度：O(N) ，其中 N 是链表中节点的数目。
- 空间复杂度：O(N) 。如果我们仔细分析，我们需要维护一个回溯的栈，同时也需要记录已经被深拷贝过的节点，也就是维护一个已访问字典。渐进时间复杂度为 O(N)。


### 2.O(N) 空间的迭代
**思路：**
![](https://pic.leetcode-cn.com/203559119fb45aa1bb844a5441ce18089f4005fa386bd794048c51fd25686e87-image.png)

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
public class Solution {
  // Visited dictionary to hold old node reference as "key" and new node reference as the "value"
  HashMap<Node, Node> visited = new HashMap<Node, Node>();

  public Node getClonedNode(Node node) {
    // If the node exists then
    if (node != null) {
      // Check if the node is in the visited dictionary
      if (this.visited.containsKey(node)) {
        // If its in the visited dictionary then return the new node reference from the dictionary
        return this.visited.get(node);
      } else {
        // Otherwise create a new node, add to the dictionary and return it
        this.visited.put(node, new Node(node.val, null, null));
        return this.visited.get(node);
      }
    }
    return null;
  }

  public Node copyRandomList(Node head) {

    if (head == null) {
      return null;
    }

    Node oldNode = head;

    // Creating the new head node.
    Node newNode = new Node(oldNode.val);
    this.visited.put(oldNode, newNode);

    // Iterate on the linked list until all nodes are cloned.
    while (oldNode != null) {
      // Get the clones of the nodes referenced by random and next pointers.
      newNode.random = this.getClonedNode(oldNode.random);
      newNode.next = this.getClonedNode(oldNode.next);

      // Move one step ahead in the linked list.
      oldNode = oldNode.next;
      newNode = newNode.next;
    }
    return this.visited.get(head);
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N) 。因为我们需要将原链表逐一遍历。
- 空间复杂度：O(N)。 我们需要维护一个字典，保存旧的节点和新的节点的对应。因此总共需要 N 个节点，需要 O(N) 的空间复杂度。

### 2.O(1) 空间的迭代
**思路：**
![](https://pic.leetcode-cn.com/62ba6efc1d3a77ba04956a105eeaa5738ef1771d9e2fc9f4daf80a0cf1275d70-image.png)
![](https://pic.leetcode-cn.com/1789e6dd9bbe41223cab82b2e0a7615cd1a8ed16a3c992462d4e1eaec3b82fb1-image.png)
![](https://pic.leetcode-cn.com/a28323ef84883ec02e7d99fd13b444dede9355389c7567e43e7ee1c85262a2d3-image.png)

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
public class Solution {
  public Node copyRandomList(Node head) {

    if (head == null) {
      return null;
    }

    // Creating a new weaved list of original and copied nodes.
    Node ptr = head;
    while (ptr != null) {

      // Cloned node
      Node newNode = new Node(ptr.val);

      // Inserting the cloned node just next to the original node.
      // If A->B->C is the original linked list,
      // Linked list after weaving cloned nodes would be A->A'->B->B'->C->C'
      newNode.next = ptr.next;
      ptr.next = newNode;
      ptr = newNode.next;
    }

    ptr = head;

    // Now link the random pointers of the new nodes created.
    // Iterate the newly created list and use the original nodes' random pointers,
    // to assign references to random pointers for cloned nodes.
    while (ptr != null) {
      ptr.next.random = (ptr.random != null) ? ptr.random.next : null;
      ptr = ptr.next.next;
    }

    // Unweave the linked list to get back the original linked list and the cloned list.
    // i.e. A->A'->B->B'->C->C' would be broken to A->B->C and A'->B'->C'
    Node ptr_old_list = head; // A->B->C
    Node ptr_new_list = head.next; // A'->B'->C'
    Node head_old = head.next;
    while (ptr_old_list != null) {
      ptr_old_list.next = ptr_old_list.next.next;
      ptr_new_list.next = (ptr_new_list.next != null) ? ptr_new_list.next.next : null;
      ptr_old_list = ptr_old_list.next;
      ptr_new_list = ptr_new_list.next;
    }
    return head_old;
  }
}

```
**复杂度分析：**
- 时间复杂度：O(N)。
- 空间复杂度：O(1)。



## 其他题解
### 1.拷贝 next 保存
**思路：**
![](https://pic.leetcode-cn.com/4bc12694524ee548153e207fd069607af8299530bb2a2f3690c68f7b86d91e2b-1563690472002.png)

```
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        // 复制
        Node cur = head;
        while (cur != null) {
            Node tmp = cur.next;
            cur.next = new Node(cur.val, null, null );
            cur.next.next = tmp;
            cur = tmp;
        }
        // 置随机指针
        cur = head;
        while (cur != null) {
            if (cur.random != null) cur.next.random = cur.random.next;
            cur = cur.next.next;
        }
        // 拆分
        cur = head;
        Node copy_head = cur.next;
        Node copy_cur = copy_head;
        while (copy_cur.next != null) {
            cur.next = cur.next.next;
            cur = cur.next;

            copy_cur.next = copy_cur.next.next;
            copy_cur = copy_cur.next;
        }
        // 结束标志null
        cur.next = null;
        return copy_head;
    }
}

```


```/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/

/*分三步进行
1. 复制链表 把克隆节点放在原节点后面
2. 重构克隆链表的随机指针
3. 拆分链表

*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;

        //使用头结点 特例不用单独处理
        Node root = new Node();
        root.next = head;

        cloneNodes(root);
        connectRandomNodes(root);
        return reconnectNodes(root);
    }

    public void cloneNodes(Node root){
        Node pNode = root.next;
        while(pNode != null){
            Node pCloned = new Node();
            pCloned.val = pNode.val;
            pCloned.next = pNode.next;

            pNode.next = pCloned;

            pNode = pCloned.next;
        }
    }

    public void connectRandomNodes(Node root){
        Node pNode = root.next;

        while(pNode != null){
            Node pCloned = pNode.next;
            if(pNode.random != null){
                pCloned.random = pNode.random.next;
            }
            pNode = pCloned.next;
        }
    }

    public Node reconnectNodes(Node root){
        Node pNode = root.next;
        Node pClonedHead = pNode.next;
        Node pCloned = pClonedHead;

        pNode.next = pCloned.next;
        pNode = pNode.next;

        //pNode提前一步 方便指示cloneNode的连接位置
        while(pNode != null){
            pCloned.next = pNode.next;
            pCloned = pCloned.next;

            pNode.next = pCloned.next;
            pNode = pNode.next;
        }
        return pClonedHead;
    }
}
```

### 2.拷贝 random 保存
**思路：**
![](https://pic.leetcode-cn.com/9d18d01597f5ca7562c8dd3908082b13c27b989fcaebb37c163d6e7ced65f412.jpg)

```
public Node copyRandomList(Node head) {
    if (head == null) {
        return null;
    }
    Node l1 = head;
    Node l2 = null;
    //生成所有的节点，讲它们保存到原链表的 random 域，
    //同时利用新生成的节点的 next 域保存原链表的 random。
    while (l1 != null) {
        l2 = new Node();
        l2.val = l1.val;
        l2.next = l1.random;
        l1.random = l2;
        l1 = l1.next;
    }
    l1 = head;
    //更新新生成节点的 random 指针。
    while (l1 != null) {
        l2 = l1.random;
        l2.random = l2.next != null ? l2.next.random : null;
        l1 = l1.next;
    }

    l1 = head;
    Node l2_head = l1.random;
    //恢复原链表的 random 指针，同时更新新生成节点的 next 指针。
    while (l1 != null) {
        l2 = l1.random;
        l1.random = l2.next;
        l2.next = l1.next != null ? l1.next.random : null;
        l1 = l1.next;
    }
    return l2_head;
}

```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/copy-list-with-random-pointer/solution/fu-zhi-dai-sui-ji-zhi-zhen-de-lian-biao-by-leetcod/)
[powcai](https://leetcode-cn.com/problems/copy-list-with-random-pointer/solution/duo-chong-si-lu-by-powcai/)
[windliang](https://leetcode-cn.com/problems/copy-list-with-random-pointer/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-32/)***
