---
title: 210.课程表 II（Course Schedule II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [210\. 课程表 II](https://leetcode-cn.com/problems/course-schedule-ii/)

Difficulty: **中等**


现在你总共有 _n_ 门课需要选，记为 `0` 到 `n-1`。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: `[0,1]`

给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。

**示例 1:**

```
输入: 2, [[1,0]]
输出: [0,1]
解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。
```

**示例 2:**

```
输入: 4, [[1,0],[2,0],[3,1],[3,2]]
输出: [0,1,2,3] or [0,2,1,3]
解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
     因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。
```

**说明:**

1.  输入的先决条件是由**边缘列表**表示的图形，而不是邻接矩阵。详情请参见。
2.  你可以假定输入的先决条件中没有重复的边。

**提示:**

1.  这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
2.  - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
3.  拓扑排序也可以通过  完成。


#### Solution1 - 深度优先搜索
![](https://pic.leetcode-cn.com/6d3c1126d636f52c38f59b7df8994a7e1c10fa8b7ed68791246308a7b5b4e561-image.png)
Language: **Java**

```java
​class Solution {
  static int WHITE = 1;
  static int GRAY = 2;
  static int BLACK = 3;

  boolean isPossible;
  Map<Integer, Integer> color;
  Map<Integer, List<Integer>> adjList;
  List<Integer> topologicalOrder;

  private void init(int numCourses) {
    this.isPossible = true;
    this.color = new HashMap<Integer, Integer>();
    this.adjList = new HashMap<Integer, List<Integer>>();
    this.topologicalOrder = new ArrayList<Integer>();

    // By default all vertces are WHITE
    for (int i = 0; i < numCourses; i++) {
      this.color.put(i, WHITE);
    }
  }

  private void dfs(int node) {

    // Don't recurse further if we found a cycle already
    if (!this.isPossible) {
      return;
    }

    // Start the recursion
    this.color.put(node, GRAY);

    // Traverse on nei***oring vertices
    for (Integer nei***or : this.adjList.getOrDefault(node, new ArrayList<Integer>())) {
      if (this.color.get(nei***or) == WHITE) {
        this.dfs(nei***or);
      } else if (this.color.get(nei***or) == GRAY) {
        // An edge to a GRAY vertex represents a cycle
        this.isPossible = false;
      }
    }

    // Recursion ends. We mark it as black
    this.color.put(node, BLACK);
    this.topologicalOrder.add(node);
  }

  public int[] findOrder(int numCourses, int[][] prerequisites) {

    this.init(numCourses);

    // Create the adjacency list representation of the graph
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> lst = adjList.getOrDefault(src, new ArrayList<Integer>());
      lst.add(dest);
      adjList.put(src, lst);
    }

    // If the node is unprocessed, then call dfs on it.
    for (int i = 0; i < numCourses; i++) {
      if (this.color.get(i) == WHITE) {
        this.dfs(i);
      }
    }

    int[] order;
    if (this.isPossible) {
      order = new int[numCourses];
      for (int i = 0; i < numCourses; i++) {
        order[i] = this.topologicalOrder.get(numCourses - i - 1);
      }
    } else {
      order = new int[0];
    }

    return order;
  }
}

```

#### Solution2 - 利用结点的入度
![](https://pic.leetcode-cn.com/48020b1ad252572469efd8749cf9959b2aad49dacc8d0eed4b95703af378139b-image.png)
Language: **Java**

```java
​class Solution {
  public int[] findOrder(int numCourses, int[][] prerequisites) {

    boolean isPossible = true;
    Map<Integer, List<Integer>> adjList = new HashMap<Integer, List<Integer>>();
    int[] indegree = new int[numCourses];
    int[] topologicalOrder = new int[numCourses];

    // Create the adjacency list representation of the graph
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> lst = adjList.getOrDefault(src, new ArrayList<Integer>());
      lst.add(dest);
      adjList.put(src, lst);

      // Record in-degree of each vertex
      indegree[dest] += 1;
    }

    // Add all vertices with 0 in-degree to the queue
    Queue<Integer> q = new LinkedList<Integer>();
    for (int i = 0; i < numCourses; i++) {
      if (indegree[i] == 0) {
        q.add(i);
      }
    }

    int i = 0;
    // Process until the Q becomes empty
    while (!q.isEmpty()) {
      int node = q.remove();
      topologicalOrder[i++] = node;

      // Reduce the in-degree of each nei***or by 1
      if (adjList.containsKey(node)) {
        for (Integer nei***or : adjList.get(node)) {
          indegree[nei***or]--;

          // If in-degree of a nei***or becomes 0, add it to the Q
          if (indegree[nei***or] == 0) {
            q.add(nei***or);
          }
        }
      }
    }

    // Check to see if topological sort is possible or not.
    if (i == numCourses) {
      return topologicalOrder;
    }

    return new int[0];
  }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/course-schedule-ii/solution/ke-cheng-biao-ii-by-leetcode/)***
