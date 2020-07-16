---
title: 542. 01 矩阵 (01 Matrix)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [542\. 01 矩阵](https://leetcode-cn.com/problems/01-matrix/)

Difficulty: **中等**


给定一个由 0 和 1 组成的矩阵，找出每个元素到最近的 0 的距离。

两个相邻元素间的距离为 1 。

**示例 1:**  
输入:

```
0 0 0
0 1 0
0 0 0
```

输出:

```
0 0 0
0 1 0
0 0 0
```

**示例 2:**  
输入:

```
0 0 0
0 1 0
1 1 1
```

输出:

```
0 0 0
0 1 0
1 2 1
```

**注意:**

1.  给定矩阵的元素个数不超过 10000。
2.  给定矩阵中至少有一个元素是 0。
3.  矩阵中的元素只在四个方向上相邻: 上、下、左、右。


#### Solution

Language: **Java**

```java
​class Solution {
    public int[][] updateMatrix(int[][] matrix) {
  int height = matrix.length;
        int width = matrix[0].length;
        int[] indexs = new int[height*width*2];
        int count = 0;
        for(int rowIndex=0;rowIndex<height;rowIndex++) {
            for (int columnIndex = 0; columnIndex < width; columnIndex++) {
                // 元素值为1才需要更新层级
                if(matrix[rowIndex][columnIndex] == 1) {
                    // 元素与0相邻，则不用更新层级（因为本来就是是1了）
                    if((columnIndex-1 >= 0 && matrix[rowIndex][columnIndex-1] == 0)
                        || (rowIndex-1 >= 0 && matrix[rowIndex-1][columnIndex] == 0)
                        || (columnIndex+1 < width && matrix[rowIndex][columnIndex+1] == 0)
                        || (rowIndex+1 < height && matrix[rowIndex+1][columnIndex] == 0)) {
                        continue;
                    }
                    // 元素本身层级为1，且不与0相邻，则元素层级+1
                    //（本身就是1，因此直接赋值2，其实用++也行）
                    matrix[rowIndex][columnIndex] = 2;
                    // 记录横纵坐标
                    indexs[count++] = rowIndex;
                    indexs[count++] = columnIndex;
                }
            }
        }
        // 待检测的深度记录为1（意思是，如果有元素与该深度相邻，则元素的深度为attach+1）
        int attach = 1;
        // 横纵坐标数大于1个（2个为一组）
        while(count>2) {
            // 记录待检查的横纵坐标数
            int len=count;
            // 清空下一层横纵坐标数
            count = 0;
            for(int rowIndex,columnIndex,i=0;i<len;i+=2){
                rowIndex = indexs[i];
                columnIndex = indexs[i+1];
                // 元素与attach相邻，则不用更新元素层级（元素值本身已经是attach+1）
                if((columnIndex-1 >= 0 && matrix[rowIndex][columnIndex-1] == attach)
                    || (rowIndex-1 >= 0 && matrix[rowIndex-1][columnIndex] == attach)
                    || (columnIndex+1 < width && matrix[rowIndex][columnIndex+1] == attach)
                    || (rowIndex+1 < height && matrix[rowIndex+1][columnIndex] == attach)) {
                    continue;
                }
                // 元素本身层级为attach+1，且不与attach相邻，则元素层级+1
                //（本身已经是attach+1，因此直接赋值已经是attach+2，其实用++也行）
                matrix[rowIndex][columnIndex] = attach+2;
                // 记录横纵坐标
                indexs[count++] = rowIndex;
                indexs[count++] = columnIndex;
            }
            // 层级深度+1
            attach++;
        }
        return matrix;

    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/01-matrix/)***
