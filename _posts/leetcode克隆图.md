---
title: 133. 克隆图（Clone Graph）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定无向连通图中一个节点的引用，返回该图的深拷贝（克隆）。图中的每个节点都包含它的值 val（Int） 和其邻居的列表（list[Node]）。

示例：
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/23/113_sample.png)

```
输入：
{"$id":"1","neighbors":[{"$id":"2","neighbors":[{"$ref":"1"},{"$id":"3","neighbors":[{"$ref":"2"},{"$id":"4","neighbors":[{"$ref":"3"},{"$ref":"1"}],"val":4}],"val":3}],"val":2},{"$ref":"4"}],"val":1}

解释：
节点 1 的值是 1，它有两个邻居：节点 2 和 4 。
节点 2 的值是 2，它有两个邻居：节点 1 和 3 。
节点 3 的值是 3，它有两个邻居：节点 2 和 4 。
节点 4 的值是 4，它有两个邻居：节点 1 和 3 。
```

提示：

1. 节点数介于 1 到 100 之间。
2. 无向图是一个简单图，这意味着图中没有重复的边，也没有自环。
3. 由于图是无向的，如果节点 p 是节点 q 的邻居，那么节点 q 也必须是节点 p 的邻居。
4. 必须将给定节点的拷贝作为对克隆图的引用返回。



# 题解

## 官方题解
暂无


## 其他题解

### 1.BFS
**思路：** 第一种可以两遍遍历，第一次创建节点，第二次创建联系；第二种一遍遍历，利用 map 记录。


```
public Node cloneGraph(Node node) {
    if (node == null) {
        return node;
    }
    Queue<Node> queue = new LinkedList<>();
    Map<Integer, Node> map = new HashMap<>();
    queue.offer(node);
    //先生成第一个节点
    Node n = new Node();
    n.val = node.val;
    n.neighbors = new ArrayList<Node>();
    map.put(n.val, n);
    while (!queue.isEmpty()) {
        Node cur = queue.poll();
        for (Node temp : cur.neighbors) {
            //没有生成的节点就生成
            if (!map.containsKey(temp.val)) {
                n = new Node();
                n.val = temp.val;
                n.neighbors = new ArrayList<Node>();
                map.put(n.val, n);
                queue.offer(temp);
            }
            map.get(cur.val).neighbors.add(map.get(temp.val));
        }
    }

    return map.get(node.val);
}
```

### 2.DFS
**思路：**


```
public Node cloneGraph(Node node) {
    if (node == null) {
        return node;
    }
    Map<Integer, Node> map = new HashMap<>();
    return cloneGrapthHelper(node, map);
}

private Node cloneGrapthHelper(Node node, Map<Integer, Node> map) {
    if (map.containsKey(node.val)) {
        return map.get(node.val);
    }
    //生成当前节点
    Node n = new Node();
    n.val = node.val;
    n.neighbors = new ArrayList<Node>();
    map.put(node.val, n);
    //添加它的所有邻居节点
    for (Node temp : node.neighbors) {
        n.neighbors.add(cloneGrapthHelper(temp, map));
    }
    return n;
}
```

```
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;

    public Node() {}

    public Node(int _val,List<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/
class Solution {
    public Node cloneGraph(Node node) {
        Map<Node, Node> created = new HashMap<>();
        return cloneGraph(node, created);
    }

    public Node cloneGraph(Node node, Map<Node, Node> created ) {
        if (created.containsKey(node)) {
            return created.get(node);
        }

        Node newNode = new Node(node.val, new ArrayList<>());
        created.put(node, newNode);
        for (Node n : node.neighbors) {
            newNode.neighbors.add(cloneGraph(n, created));
        }
        return newNode;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/clone-graph/submissions/)
[windliang](https://leetcode-cn.com/problems/clone-graph/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-9/)***
