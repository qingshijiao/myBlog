---
title: 310.最小高度树（Minimum Height Trees）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [310\. 最小高度树](https://leetcode-cn.com/problems/minimum-height-trees/)

Difficulty: **中等**


对于一个具有树特征的无向图，我们可选择任何一个节点作为根。图因此可以成为树，在所有可能的树中，具有最小高度的树被称为最小高度树。给出这样的一个图，写出一个函数找到所有的最小高度树并返回他们的根节点。

**格式**

该图包含 `n` 个节点，标记为 `0` 到 `n - 1`。给定数字 `n` 和一个无向边 `edges` 列表（每一个边都是一对标签）。

你可以假设没有重复的边会出现在 `edges` 中。由于所有的边都是无向边， `[0, 1]`和 `[1, 0]` 是相同的，因此不会同时出现在 `edges` 里。

**示例 1:**

```
输入: n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3

输出: [1]
```

**示例 2:**

```
输入: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5

输出: [3, 4]
```

**说明**:

*   根据，树是一个无向图，其中任何两个顶点只通过一条路径连接。 换句话说，一个任何没有简单环路的连通图都是一棵树。
*   树的高度是指根节点和叶子节点之间最长向下路径上边的数量。


#### Solution

Language: **Java**

```java
class Solution {
     public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> res = new ArrayList<>();
        int[][] gra = new int[n][];
        for(int[] edge : edges) {
            int a = edge[0], b = edge[1];
            if(gra[a] == null) gra[a] = edge;
            else gra[b] = edge;
        }
        int root = getRoot(gra);
        int[] node = getNode(gra, root);
        root = reverse(gra, root, node[0]);
        node = getNode(gra, root);

        //System.out.println(root + "/" + node[0] + ":" + node[1]);

        int len = node[1] / 2;
        int p = node[0];
        while(len-- != 0) p = getNext(gra, p);
        res.add(p);
        if((node[1] & 1) == 1) res.add(getNext(gra, p));

        return res;
    }

    private int reverse(int[][] gra, int root, int p) {
        int ret = p;
        int[] pre = null;
        while(p != root) {
            int next = getNext(gra, p);
            int[] temp = gra[p];
            gra[p] = pre;
            pre = temp;
            p = next;
        }
        gra[root] = pre;
        return ret;
    }

    private int[] getNode(int[][] gra, int root) {
        int n = gra.length;
        int max = 0, node = 0;
        int[] h = new int[n];
        int[] stack = new int[n];
        int size = 0;
        for(int i = 0; i < n; i++) {
            int p = i, count = 0;
            while(p != root && h[p] == 0) {
                stack[size++] = p;
                p = getNext(gra, p);
            }
            while(size != 0) {
                int temp = stack[--size];
                h[temp] = h[p] + 1;
                if(h[temp] > max) {
                    max = h[temp];
                    node = temp;
                }
                p = temp;
            }
        }
        return new int[]{node, h[node]};
    }

    private int getRoot(int[][] gra) {
        int p = 0;
        while(gra[p] != null) p = getNext(gra, p);
        return p;
    }

    private int getNext(int[][] gra, int p) {
        int[] ret = gra[p];
        return ret[0] == p ? ret[1] : ret[0];
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/minimum-height-trees/submissions/)***
