---
title: 454. 四数相加 II（4Sum II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [454\. 4Sum II](https://leetcode-cn.com/problems/4sum-ii/)

Difficulty: **中等**


给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 `(i, j, k, l)` ，使得 `A[i] + B[j] + C[k] + D[l] = 0`。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -2<sup>28</sup> 到 2<sup>28</sup> - 1 之间，最终结果不会超过 2<sup>31</sup> - 1 。

**例如:**

```
输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2

解释:
两个元组如下:
1\. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2\. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```


#### Solution

Language: **Java**

```java
​class Solution {

    public class Node {

        private int value;
        private int visit;
        private Node next;

        public Node(int value) {
            this.value = value;
        }

        public Node(int value, int visit, Node next) {
            this.value = value;
            this.visit = visit;
            this.next = next;
        }

        public Node insert(Node head, int value) {
            return new Node(value, 0, head);
        }
    }

    public class HashMap {

        private int max = 2 << 17;
        private int hashKey = max - 1;
        private Node[] myHash = new Node[max];

        public HashMap(int random) {
        }

        // a % (2^n) 等价于 a & (2^n - 1)
        public int getKey(int value) {
            value = (value < 0 ? -value : value);
            return (value ^ (value >>> 16)) & hashKey;
        }

        public void insert(int value) {
            int key = getKey(value);
            if (myHash[key] == null) {
                myHash[key] = new Node(value, 1, null);
                return;
            }
            Node head = myHash[key];
            while (head != null) {
                if (head.value == value) {
                    head.visit++;
                    return;
                }
                head = head.next;
            }
            myHash[key] = myHash[key].insert(myHash[key], value);
            myHash[key].visit = 1;
        }

        public int find(int value) {
            int count = 0, key = getKey(value);
            Node head = myHash[key];
            while (head != null) {
                if (head.value == value) {
                    return head.visit;
                }
                head = head.next;
            }
            return count;
        }
    }

    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        int length = C.length;
        if (length < 1) return 0;
        HashMap map = new HashMap(B[0]);
        int count = 0, i, j, sum;

        for (i = 0; i < length; i++) {
            int i1 = C[i];
            for (j = 0; j < length; j++) {
                map.insert(i1 + D[j]);
            }
        }

        for (i = 0; i < length; i++) {
            sum = -A[i];
            for (j = 0; j < length; j++) {
                count += map.find(sum - B[j]);
            }
        }
        return count;
    }

}
```


---
***参考：
[leetcode](https://leetcode-cn.com/problems/4sum-ii/)***
