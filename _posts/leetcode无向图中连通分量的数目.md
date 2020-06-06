---
title: 323.无向图中连通分量的数目

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
## 题目描述
给定编号从 0 到 n-1 的 n 个节点和一个无向边列表（每条边都是一对节点），请编写一个函数来计算无向图中连通分量的数目。

示例 1:
```
输入: n = 5 和 edges = [[0, 1], [1, 2], [3, 4]]

 0          3
 |          |
 1 --- 2    4
1
2
3
输出: 2
```
示例 2:
```
输入: n = 5 和 edges = [[0, 1], [1, 2], [2, 3], [3, 4]]

 0           4
 |           |
 1 --- 2 --- 3
1
2
3
输出: 1
```
**注意:**
你可以假设在 edges 中不会出现重复的边。而且由于所以的边都是无向边，[0, 1] 与 [1, 0] 相同，所以它们不会同时在 edges 中出现。


#### Solution1 - dfs

Language: **python**

```python
​class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        from collections import defaultdict
        graph = defaultdict(list)

        for x, y in edges:
            graph[x].append(y)
            graph[y].append(x)

        visited = set()

        def dfs(i):
            visited.add(i)
            for j in graph[i]:
                if j not in visited:
                    dfs(j)

        res = 0
        for i in range(n):
            if i not in visited:
                res += 1
                dfs(i)
        return res
```

#### Solution2 - bfs

Language: **python**

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        from collections import defaultdict, deque
        graph = defaultdict(list)

        for x, y in edges:
            graph[x].append(y)
            graph[y].append(x)

        visited = set()

        def bfs(i):
            queue = deque([i])
            while queue:
                i = queue.pop()
                for j in graph[i]:
                    if j not in visited:
                        visited.add(j)
                        queue.appendleft(j)

        res = 0
        for i in range(n):
            if i not in visited:
                res += 1
                visited.add(i)
                bfs(i)
        return res
```

#### Solution3 - 并查集

Language: **python**

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        f = {}

        def find(x):
            f.setdefault(x, x)
            if x != f[x]:
                f[x] = find(f[x])
            return f[x]

        def union(x, y):
            f[find(x)] = find(y)

        for x, y in edges:
            union(x, y)

        return len(set(find(x) for x in range(n)))
```

---
***参考:
[九四干](https://zhuanlan.zhihu.com/p/90907170)***
