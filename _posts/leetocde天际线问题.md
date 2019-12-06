---
title: 218.天际线问题（The Skyline Problem）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [218\. 天际线问题](https://leetcode-cn.com/problems/the-skyline-problem/)

Difficulty: **困难**


城市的天际线是从远处观看该城市中所有建筑物形成的轮廓的外部轮廓。现在，假设您获得了城市风光照片（图A）上**显示的所有建筑物的位置和高度**，请编写一个程序以输出由这些建筑物**形成的天际线**（图B）。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/skyline1.png)

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/skyline2.png)

每个建筑物的几何信息用三元组 `[Li，Ri，Hi]` 表示，其中 `Li` 和 `Ri` 分别是第 i 座建筑物左右边缘的 x 坐标，`Hi` 是其高度。可以保证 `0 ≤ Li, Ri ≤ INT_MAX`, `0 < Hi ≤ INT_MAX` 和 `Ri - Li > 0`。您可以假设所有建筑物都是在绝对平坦且高度为 0 的表面上的完美矩形。

例如，图A中所有建筑物的尺寸记录为：`[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ]` 。

输出是以 `[ [x1,y1], [x2, y2], [x3, y3], ... ]` 格式的“**关键点**”（图B中的红点）的列表，它们唯一地定义了天际线。**关键点是水平线段的左端点**。请注意，最右侧建筑物的最后一个关键点仅用于标记天际线的终点，并始终为零高度。此外，任何两个相邻建筑物之间的地面都应被视为天际线轮廓的一部分。

例如，图B中的天际线应该表示为：`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`。

**说明:**

- 任何输入列表中的建筑物数量保证在 `[0, 10000]` 范围内。
- 输入列表已经按左 `x` 坐标 `Li`  进行升序排列。
- 输出列表必须按 x 位排序。
- 输出天际线中不得有连续的相同高度的水平线。例如 `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` 是不正确的答案；三条高度为 5 的线应该在最终输出中合并为一个：`[...[2 3], [4 5], [12 7], ...]`


#### Solution1 - 分治
![](https://pic.leetcode-cn.com/5e0dfac6c937d4a03fec3955cbc3592456ae752ed281bc1761a33ae73b2f86ed-image.png)
![](https://pic.leetcode-cn.com/707d3e7617b5ebe4394a4d3c4db19a0c7d13c760efcc275da15ab051a66fc820-image.png)
![](https://pic.leetcode-cn.com/ad238838091649b65b9702108ce43a74a8f44176eeee8a51fdcdde594bcdedb3-image.png)
Language: **Java**

```java
​class Solution {
  /**
   *  Divide-and-conquer algorithm to solve skyline problem,
   *  which is similar with the merge sort algorithm.
   */
  public List<List<Integer>> getSkyline(int[][] buildings) {
    int n = buildings.length;
    List<List<Integer>> output = new ArrayList<List<Integer>>();

    // The base cases
    if (n == 0) return output;
    if (n == 1) {
      int xStart = buildings[0][0];
      int xEnd = buildings[0][1];
      int y = buildings[0][2];

      output.add(new ArrayList<Integer>() {{add(xStart); add(y); }});
      output.add(new ArrayList<Integer>() {{add(xEnd); add(0); }});
      // output.add(new int[]{xStart, y});
      // output.add(new int[]{xEnd, 0});
      return output;
    }

    // If there is more than one building,
    // recursively divide the input into two subproblems.
    List<List<Integer>> leftSkyline, rightSkyline;
    leftSkyline = getSkyline(Arrays.copyOfRange(buildings, 0, n / 2));
    rightSkyline = getSkyline(Arrays.copyOfRange(buildings, n / 2, n));

    // Merge the results of subproblem together.
    return mergeSkylines(leftSkyline, rightSkyline);
  }

  /**
   *  Merge two skylines together.
   */
  public List<List<Integer>> mergeSkylines(List<List<Integer>> left, List<List<Integer>> right) {
    int nL = left.size(), nR = right.size();
    int pL = 0, pR = 0;
    int currY = 0, leftY = 0, rightY = 0;
    int x, maxY;
    List<List<Integer>> output = new ArrayList<List<Integer>>();

    // while we're in the region where both skylines are present
    while ((pL < nL) && (pR < nR)) {
      List<Integer> pointL = left.get(pL);
      List<Integer> pointR = right.get(pR);
      // pick up the smallest x
      if (pointL.get(0) < pointR.get(0)) {
        x = pointL.get(0);
        leftY = pointL.get(1);
        pL++;
      }
      else {
        x = pointR.get(0);
        rightY = pointR.get(1);
        pR++;
      }
      // max height (i.e. y) between both skylines
      maxY = Math.max(leftY, rightY);
      // update output if there is a skyline change
      if (currY != maxY) {
        updateOutput(output, x, maxY);
        currY = maxY;
      }
    }

    // there is only left skyline
    appendSkyline(output, left, pL, nL, currY);

    // there is only right skyline
    appendSkyline(output, right, pR, nR, currY);

    return output;
  }

  /**
   * Update the final output with the new element.
   */
  public void updateOutput(List<List<Integer>> output, int x, int y) {
    // if skyline change is not vertical -
    // add the new point
    if (output.isEmpty() || output.get(output.size() - 1).get(0) != x)
      output.add(new ArrayList<Integer>() {{add(x); add(y); }});
      // if skyline change is vertical -
      // update the last point
    else {
      output.get(output.size() - 1).set(1, y);
    }
  }

  /**
   *  Append the rest of the skyline elements with indice (p, n)
   *  to the final output.
   */
  public void appendSkyline(List<List<Integer>> output, List<List<Integer>> skyline,
                            int p, int n, int currY) {
    while (p < n) {
      List<Integer> point = skyline.get(p);
      int x = point.get(0);
      int y = point.get(1);
      p++;

      // update output
      // if there is a skyline change
      if (currY != y) {
        updateOutput(output, x, y);
        currY = y;
      }
    }
  }
}

```

#### Solution2 - 扫描栈
![](https://pic.leetcode-cn.com/0bf43198e107719f1dbdbda82a7d213d87019200b4288a11bf49822d7646a4b1-skyline.gif)

Language: **c++**

```c++
class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int,int>> h;
        multiset<int> m;
        vector<vector<int>> res;

        //1、将每一个建筑分成“两个部分”，例如:[2,9,10]可以转换成[2，-10][9,10]，我们用负值来表示左边界
        for(const auto& b:buildings)
        {
            h.push_back({b[0], -b[2]});
            h.push_back({b[1], b[2]});
        }

        //2、根据x值对分段进行排序
        sort(h.begin(),h.end());
        int prev = 0, cur = 0;
        m.insert(0);

        3、遍历
        for (auto i:h)
        {
            if (i.second < 0) m.insert(-i.second);  //左端点，高度入堆
            else m.erase(m.find(i.second));         //右端点，高度出堆
            cur = *m.rbegin();                      //当前最大高度高度
            if (cur != prev) {                      //当前最大高度不等于最大高度perv表示这是一个转折点
                res.push_back({i.first, cur});      //添加坐标
                prev = cur;                         //更新最大高度
            }
        }
        return res;
    }
};

```

Language: **java**

```java
public List<List<Integer>> getSkyline(int[][] buildings) {
       List<List<Integer>> res = new ArrayList<>();

       Map<Integer, List<Integer>> map = new TreeMap<>();
       for (int[] build : buildings) {
           //插入左节点
           if (!map.containsKey(build[0]))
               map.put(build[0], new ArrayList<>());
           map.get(build[0]).add(-build[2]);
           //插入右节点
           if (!map.containsKey(build[1]))
               map.put(build[1], new ArrayList<>());
           map.get(build[1]).add(build[2]);
       }
       //保留当前位置的所有高度 重定义排序：从大到小
       Map<Integer, Integer> heights = new TreeMap<>(new Comparator<Integer>() {
           @Override
           public int compare(Integer o1, Integer o2) {
               return o2 - o1;
           }
       });
       //保留上一个位置的横坐标及高度
       int[] last = {0, 0};

       for (int key : map.keySet()) {
//            Integer[] yArrays =(Integer[]) map.get(key).toArray();
           List<Integer> yArrays = map.get(key);
           //排序
           Collections.sort(yArrays);

           for (int y : yArrays) {
               //左端点,高度入队
               if (y < 0) {
                   int val = heights.getOrDefault(-y, 0);
                   heights.put(-y, val + 1);
               } else {
                   //右端点移除高度
                   int val = heights.getOrDefault(y, 0);
                   if (val == 1)
                       heights.remove(y);
                   else
                       heights.put(y, val - 1);
               }
               //获取heights的最大值:就是第一个值
               Integer maxHeight = 0;
               if (!heights.isEmpty())
                   maxHeight = heights.keySet().iterator().next();

               //如果当前最大高度不同于上一个高度，说明其为转折点
               if (last[1] != maxHeight) {
                   //更新last，并加入结果集
                   last[0] = key;
                   last[1] = maxHeight;
                   res.add(Arrays.asList(key, maxHeight));
               }
           }
       }

       return res;
   }

```

```java
class Solution {
    static class Building {
        int loc;
        int height;
        int type;

        public Building(int loc, int height, int type) {
            this.loc = loc;
            this.height = height;
            this.type = type;
        }
    }

    public List<List<Integer>> getSkyline(int[][] buildings) {
        List<List<Integer>> res = new ArrayList<>();
        //默认输入已经按照起点排序
        //按照高度降序，同高度根据起点升序
        PriorityQueue<int[]> heightHeap = new PriorityQueue<>(new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[2] == b[2] ? a[0] - b[0] : b[2] - a[2];
            }
        });

        //默认起点，PRE保存前面能看见的最高建筑和他的终点起点
        int[] pre = new int[]{Integer.MIN_VALUE, Integer.MAX_VALUE, 0};
        for (int[] b : buildings) {
            // 当出现断点情况，需要清空之前建筑群
            while (!heightHeap.isEmpty() && b[0] > pre[1]) {
                //获取之前最高建筑
                int[] curHighest = heightHeap.poll();
                //如果最高的终点在PRE之前，说明已经处理
                if (curHighest[1] <= pre[1]) continue;
                //如果遇到PRE之后的点，加入结果并更新PRE
                res.add(Arrays.asList(pre[1], curHighest[2]));
                pre = curHighest;
            }

            //当前建筑比之前建筑高
            if (b[2] > pre[2]) {
                if (b[0] == pre[0]) {
                    //同起点情况下，矮建筑必然被挡住，直接删除
                    res.remove(res.size() - 1);
                }
                res.add(Arrays.asList(b[0], b[2])); //未被之后遮挡前先加入结果
                if (b[1] < pre[1]) {
                    heightHeap.offer(pre); //如果终点小于前终点，将前值入堆
                }
                pre = b;//更新前值因为发现了更高的
            } else if (b[2] == pre[2]) { //同高度继续延伸END
                pre[1] = b[1];
            } else if (b[1] > pre[1]) {
                heightHeap.offer(b); //矮建筑直接入堆
            }
        }


        while (!heightHeap.isEmpty()) {
            //如果堆不为空，重复之前操作
            int[] cur = heightHeap.poll();
            if (cur[1] <= pre[1]) continue;
            res.add(Arrays.asList(pre[1], cur[2]));
            pre = cur;
        }
        //最后有剩余
        if (pre[2] > 0) {
            res.add(Arrays.asList(pre[1], 0));
        }
        return res;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/the-skyline-problem/submissions/)
[ivan_allen](https://leetcode-cn.com/problems/the-skyline-problem/solution/218tian-ji-xian-wen-ti-sao-miao-xian-fa-by-ivan_al/)
[Bug](https://leetcode-cn.com/problems/the-skyline-problem/solution/can-kao-da-lao-de-sao-miao-xian-fa-javaban-ben-by-/)***
