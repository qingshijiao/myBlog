---
title: 207.课程表（Course Schedule）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [207\. Course Schedule](https://leetcode-cn.com/problems/course-schedule/)

Difficulty: **中等**


现在你总共有 _n_ 门课需要选，记为 `0` 到 `n-1`。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: `[0,1]`

给定课程总量以及它们的先决条件，判断是否可能完成所有课程的学习？

**示例 1:**

```
输入: 2, [[1,0]]
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
```

**示例 2:**

```
输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
```

**说明:**

1.  输入的先决条件是由**边缘列表**表示的图形，而不是邻接矩阵。详情请参见。
2.  你可以假定输入的先决条件中没有重复的边。

**提示:**

1.  这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
2.  - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
3.  拓扑排序也可以通过  完成。


#### Solution1 - 入度表（广度优先遍历）
![](https://pic.leetcode-cn.com/bd2f99fca16bd3a626153945a28ea8a75b151e6404d5525ad30202e19caab05c-Picture2.png)

Language: **Java**
time:O(m+n) space:O(n)
```java
​class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] indegrees = new int[numCourses];
        for(int[] cp : prerequisites) indegrees[cp[0]]++;
        LinkedList<Integer> queue = new LinkedList<>();
        for(int i = 0; i < numCourses; i++){
            if(indegrees[i] == 0) queue.addLast(i);
        }
        while(!queue.isEmpty()) {
            Integer pre = queue.removeFirst();
            numCourses--;
            for(int[] req : prerequisites) {
                if(req[1] != pre) continue;
                if(--indegrees[req[0]] == 0) queue.add(req[0]);
            }
        }
        return numCourses == 0;
    }
}

```

#### Solution2 - 深度优先遍历
![](https://pic.leetcode-cn.com/b2d7e9eea81fa4fa3e610a60234b893e18c16b1771ec7d9a15c22a8102b03f4f-Picture5.png)

Language: **Java**
time:O(m+n) space:O(n)
```java
​class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[][] adjacency = new int[numCourses][numCourses];
        int[] flags = new int[numCourses];
        for(int[] cp : prerequisites)
            adjacency[cp[1]][cp[0]] = 1;
        for(int i = 0; i < numCourses; i++){
            if(!dfs(adjacency, flags, i)) return false;
        }
        return true;
    }
    private boolean dfs(int[][] adjacency, int[] flags, int i) {
        if(flags[i] == 1) return false;
        if(flags[i] == -1) return true;
        flags[i] = 1;
        for(int j = 0; j < adjacency.length; j++) {
            if(adjacency[i][j] == 1 && !dfs(adjacency, flags, j)) return false;
        }
        flags[i] = -1;
        return true;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/course-schedule/)
[jyd](https://leetcode-cn.com/problems/course-schedule/solution/course-schedule-tuo-bu-pai-xu-bfsdfsliang-chong-fa/)***
