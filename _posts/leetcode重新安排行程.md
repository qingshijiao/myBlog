---
title: 332.重新安排行程 (Reconstruct Itinerary)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [332\. 重新安排行程](https://leetcode-cn.com/problems/reconstruct-itinerary/)

Difficulty: **中等**


给定一个机票的字符串二维数组 `[from, to]`，子数组中的两个成员分别表示飞机出发和降落的机场地点，对该行程进行重新规划排序。所有这些机票都属于一个从JFK（肯尼迪国际机场）出发的先生，所以该行程必须从 JFK 出发。

**说明:**

1.  如果存在多种有效的行程，你可以按字符自然排序返回最小的行程组合。例如，行程 ["JFK", "LGA"] 与 ["JFK", "LGB"] 相比就更小，排序更靠前
2.  所有的机场都用三个大写字母表示（机场代码）。
3.  假定所有机票至少存在一种合理的行程。

**示例 1:**

```
输入: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
输出: ["JFK", "MUC", "LHR", "SFO", "SJC"]
```

**示例 2:**

```
输入: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
输出: ["JFK","ATL","JFK","SFO","ATL","SFO"]
解释: 另一种有效的行程是 ["JFK","SFO","ATL","JFK","ATL","SFO"]。但是它自然排序更大更靠后。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        List<String> res = new ArrayList<>();
        if (tickets.size() == 0) {
            return res;
        }
        HashMap<String, PriorityQueue<String>> map = new HashMap<>();
        for (List<String> ticket : tickets) {
            String from = ticket.get(0);
            String to = ticket.get(1);
            if (map.get(from) == null) {
                map.put(from, new PriorityQueue<>());
            }
            map.get(from).offer(to);
        }

        findItineraryHelper(map, res, "JFK");
        return res;
    }

    public void findItineraryHelper(HashMap<String, PriorityQueue<String>> map, List<String> res, String from) {
        PriorityQueue<String> to = map.get(from);
        if (to != null) {
            while (!to.isEmpty()) {
                findItineraryHelper(map, res, to.poll());
            }
        }
        res.add(0, from);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/reconstruct-itinerary/submissions/)***
