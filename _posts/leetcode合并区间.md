---
title: 56. 合并区间（Merge Intervals）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给出一个区间的集合，请合并所有重叠的区间。

示例 1:
```
输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```
示例 2:
```
输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
```


# 题解

## 官方题解
### 1.连通块
**思路：** 如果我们画一个图，区间看成顶点，相交的区间之间连一条无向边，那么图中连通块内的所有区间都可以合并成一个。
![](https://pic.leetcode-cn.com/4773f014526c5f499e929cfd9b6fc0aaf8dad9feb1ddbed0d5836a5a2881b780-56-1.png)
```
class Solution {
    private Map<Interval, List<Interval> > graph;
    private Map<Integer, List<Interval> > nodesInComp;
    private Set<Interval> visited;

    // return whether two intervals overlap (inclusive)
    private boolean overlap(Interval a, Interval b) {
        return a.start <= b.end && b.start <= a.end;
    }

    // build a graph where an undirected edge between intervals u and v exists
    // iff u and v overlap.
    private void buildGraph(List<Interval> intervals) {
        graph = new HashMap<>();
        for (Interval interval : intervals) {
            graph.put(interval, new LinkedList<>());
        }

        for (Interval interval1 : intervals) {
            for (Interval interval2 : intervals) {
                if (overlap(interval1, interval2)) {
                    graph.get(interval1).add(interval2);
                    graph.get(interval2).add(interval1);
                }
            }
        }
    }

    // merges all of the nodes in this connected component into one interval.
    private Interval mergeNodes(List<Interval> nodes) {
        int minStart = nodes.get(0).start;
        for (Interval node : nodes) {
            minStart = Math.min(minStart, node.start);
        }

        int maxEnd = nodes.get(0).end;
        for (Interval node : nodes) {
            maxEnd= Math.max(maxEnd, node.end);
        }

        return new Interval(minStart, maxEnd);
    }

    // use depth-first search to mark all nodes in the same connected component
    // with the same integer.
    private void markComponentDFS(Interval start, int compNumber) {
        Stack<Interval> stack = new Stack<>();
        stack.add(start);

        while (!stack.isEmpty()) {
            Interval node = stack.pop();
            if (!visited.contains(node)) {
                visited.add(node);

                if (nodesInComp.get(compNumber) == null) {
                    nodesInComp.put(compNumber, new LinkedList<>());
                }
                nodesInComp.get(compNumber).add(node);

                for (Interval child : graph.get(node)) {
                    stack.add(child);
                }
            }
        }
    }

    // gets the connected components of the interval overlap graph.
    private void buildComponents(List<Interval> intervals) {
        nodesInComp = new HashMap();
        visited = new HashSet();
        int compNumber = 0;

        for (Interval interval : intervals) {
            if (!visited.contains(interval)) {
                markComponentDFS(interval, compNumber);
                compNumber++;
            }
        }
    }

    public List<Interval> merge(List<Interval> intervals) {
        buildGraph(intervals);
        buildComponents(intervals);

        // for each component, merge all intervals into one interval.
        List<Interval> merged = new LinkedList<>();
        for (int comp = 0; comp < nodesInComp.size(); comp++) {
            merged.add(mergeNodes(nodesInComp.get(comp)));
        }

        return merged;
    }
}


```
**复杂度分析：**
- 时间复杂度：O(n^2),建图的时间开销 O(V + E) = O(V) + O(E) = O(n) + O(n^2) = O(n^2)，最坏情况所有区间都相互重合，遍历整个图有相同的开销，因为 visited 数组保证了每个节点只会被访问一次。最后每个节点都恰好属于一个连通块，所以合并的时间开销是 O(V) = O(n)。总和为：O(n^2) + O(n^2) + O(n) = O(n^2)
- 空间复杂度：O(n^2), 根据之前提到的，最坏情况下每个区间都是相互重合的，所以两两区间都会有一条边，所以内存占用量是输入大小的平方级别。

### 2.排序
**思路：** 如果我们按照区间的 start 大小排序，那么在这个排序的列表中可以合并的区间一定是连续的。

![](https://i.loli.net/2019/09/23/pnXYRj5ilK2NEBy.png)


```
class Solution {
    private class IntervalComparator implements Comparator<Interval> {
        @Override
        public int compare(Interval a, Interval b) {
            return a.start < b.start ? -1 : a.start == b.start ? 0 : 1;
        }
    }

    public List<Interval> merge(List<Interval> intervals) {
        Collections.sort(intervals, new IntervalComparator());

        LinkedList<Interval> merged = new LinkedList<Interval>();
        for (Interval interval : intervals) {
            // if the list of merged intervals is empty or if the current
            // interval does not overlap with the previous, simply append it.
            if (merged.isEmpty() || merged.getLast().end < interval.start) {
                merged.add(interval);
            }
            // otherwise, there is overlap, so we merge the current and previous
            // intervals.
            else {
                merged.getLast().end = Math.max(merged.getLast().end, interval.end);
            }
        }

        return merged;
    }
}


```
**复杂度分析：**
- 时间复杂度：O(nlogn)，除去 sort 的开销，我们只需要一次线性扫描，所以主要的时间开销是排序的 O(nlgn)
- 空间复杂度：O(1) (or O(n))，如果我们可以原地排序 intervals ，就不需要额外的存储空间；否则，我们就需要一个线性大小的空间去存储 intervals 的备份，来完成排序过程。

## 其他题解
### 1.排序 + 合并
**思路：** 先排序，后合并数组
```
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();
        if (intervals == null || intervals.length == 0)
            return res.toArray(new int[0][]);

        // Arrays.sort(intervals, (a, b) -> a[0] - b[0]);// a[0] - b[0]大于0就交换顺序
        // 根据二维数组第一个数字大小按每一行整体排序
        Arrays.sort(intervals, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                // TODO Auto-generated method stub
                return o1[0] - o2[0];
            }
        });
        int i = 0;
        while (i < intervals.length) {
            int left = intervals[i][0];
            int right = intervals[i][1];
            // i不能到最后一行,所以要小于(数组的长度 - 1)
            // 判断所在行的right和下一行的left大小,对right重新进行赋最大值,之后再不断进行while循环判断
            while (i < intervals.length - 1 && right >= intervals[i + 1][0]) {
                i++;
                right = Math.max(right, intervals[i][1]);
            }
            res.add(new int[] { left, right });
            i++;
        }
        return res.toArray(new int[0][]);
    }

}
```

### 2.记录要合并的数量，将数组合并
**思路：** 
```
class Solution {
    public int[][] merge(int[][] intervals) {
        if(intervals == null || intervals.length<=1){
            return intervals;
        }
        int mergeCount = 0;
        for(int i = 0;i<intervals.length;i++){
            for(int j = i+1;j<intervals.length;j++){
                if(intervals[i][1]>=intervals[j][0] && intervals[i][0]<=intervals[j][1]){
                    if(intervals[i][1]>intervals[j][1]){
                        intervals[j][1] = intervals[i][1];
                    }
                    if(intervals[i][0]<intervals[j][0]){
                        intervals[j][0] = intervals[i][0];
                    }
                    intervals[i] = null;
                    mergeCount++;
                    break;
                }
            }
        }
        int[][] result = new int[intervals.length-mergeCount][];
        for(int i = 0,j = 0;j<intervals.length;j++){
            if(intervals[j] != null){
                result[i++] =intervals[j];
            }
        }
        return result;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/merge-intervals/solution/he-bing-qu-jian-by-leetcode/)
[spirit-9](https://leetcode-cn.com/problems/merge-intervals/solution/java-yi-dong-yi-jie-xiao-lu-gao-by-spirit-9-40/)***
