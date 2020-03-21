---
title: 311.稀疏矩阵的乘法

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given two sparse matrices A and B, return the result of AB.

You may assume that A's column number is equal to B's row number.

Example:
```
A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]

B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]


     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
```

#### Solution

Language: **Java**

```java
public int[][] multiply(int[][] A, int[][] B) {

    int[][] ret = new int[A.length][B[0].length];
    for(int i = 0; i < ret.length; ++i) {
        for(int k = 0; k < A[i].length; ++k) {
            if(A[i][k] == 0) continue;
            for(int j = 0; j < ret[i].length; ++j) {
                if(B[k][j] == 0) continue;
                ret[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    return ret;
}

```

---
***参考：
[noteanddata](http://www.noteanddata.com/leetcode-311-Sparse-Matrix-Multiplication-java-solution-note.html)***
