---
title: 406.根据身高重建队列 (Queue Reconstruction by Height)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [406\. 根据身高重建队列](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)

Difficulty: **中等**


假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对`(h, k)`表示，其中`h`是这个人的身高，`k`是排在这个人前面且身高大于或等于`h`的人数。 编写一个算法来重建这个队列。

**注意：**  
总人数少于1100人。

**示例**

```
输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int[][] reconstructQueue(int[][] people) {
        int len = people.length;
        if (len <= 1) {
            return people;
        }
        quickSort(people, 0, len - 1);
        List<int[]> list = new ArrayList<>(len);
        for (int[] item : people) {
            int k = item[1];
            list.add(k, item);
        }
        return list.toArray(new int[len][2]);
    }

    public void quickSort(int[][] people, int left, int right) {
        if (left < right) {
            int middle = divideConquer(people, left, right);
            quickSort(people, left, middle - 1);
            quickSort(people, middle + 1, right);
        }
    }

    private int divideConquer(int[][] people, int left, int right) {
        int i = left, j = right;
        int[] temp = people[i];
        while (i < j) {
            while (j > i && compare(temp, people[j]) > 0) {
                j--;
            }
            if (j > i) {
                people[i] = people[j];
                i++;
            }
            while (i < j && compare(temp, people[i]) < 0) {
                i++;
            }
            if (i < j) {
                people[j] = people[i];
                j--;
            }
        }
        people[i] = temp;
        return i;
    }

    private int compare(int[] p1, int[] p2) {
        int height1 = p1[0];
        int k1 = p1[1];
        int height2 = p2[0];
        int k2 = p2[1];
        return height1 > height2 ? 1 : height1 < height2 ? -1 : k1 < k2 ? 1 : -1;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/queue-reconstruction-by-height/submissions/)***
