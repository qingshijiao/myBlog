---
title: 53. 螺旋矩阵（Spiral Matrix）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:
```
输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]
```
示例 2:
```
输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]
```



# 题解

## 官方题解
### 1.模拟
**思路：** 绘制螺旋轨迹路径，我们发现当路径超出界限或者进入之前访问过的单元格时，会顺时针旋转方向。

假设数组有 R 行 C 列，seen[r][c] 表示第 r 行第 c 列的单元格之前已经被访问过了。当前所在位置为 (r, c)，前进方向是 di。我们希望访问所有R x C 个单元格。

当我们遍历整个矩阵，下一步候选移动位置是 (cr, cc)。如果这个候选位置在矩阵范围内并且没有被访问过，那么它将会变成下一步移动的位置；否则，我们将前进方向顺时针旋转之后再计算下一步的移动位置。


```
class Solution {
  public List<List<String>> solveNQueens(int n) {
        int[] col=new int[n];//棋子放置位置
        int[] row=new int[n];
        int[] dig=new int[2*n-1];
        int[] hill=new int[2*n-1];
        List<List<String>> answer=new ArrayList<>();
        List<List<String>> a=place(n,0,row,dig,hill,col,answer);
        return a;

    }
    List<List<String>>  place (int n,int m,int[]row,int[]dig,int [] hill,int[] col,List<List<String>> answer){
        if(n==m) {
            List<String> ans=new ArrayList<String>();

            for (int i=0;i<n;i++){
                StringBuilder sol=new StringBuilder();
                for(int j=0;j<col[i];j++){
                    sol.append('.');
                }
                sol.append('Q');
                for(int j=(col[i]+1);j<n;j++){
                    sol.append('.');
                }
                String solu=sol.toString();
                ans.add(solu);
            }
            answer.add(ans);
        }
        else{
            for(int i=0;i<n;i++) {
                int res=row[i]+dig[i+m]+hill[i-m+n-1];
                if(res==0){
                    col[m]=i;
                    row[i]=1;
                    dig[i+m]=1;
                    hill[i-m+n-1]=1;
                    place(n,(m+1),row,dig,hill,col,answer);
                    col[m]=0;
                    row[i]=0;
                    dig[i+m]=0;
                    hill[i-m+n-1]=0;
                }

            }
        }
        return answer;

    }

}

```
**复杂度分析：**
- 时间复杂度：O(N)，其中 N 是输入矩阵所有元素的个数。因为我们将矩阵中的每个元素都添加进答案里。
- 空间复杂度：O(N)，需要两个矩阵 seen 和 ans 存储所需信息。



### 2.按层模拟
**思路：** 答案是最外层所有元素按照顺时针顺序输出，其次是次外层，以此类推。

![](https://pic.leetcode-cn.com/21f4b738d3a221048ab021a8c663083b51c76a2d922c91019d6b5f514881688b-54_spiralmatrix.png)


```
class Solution {
    public List < Integer > spiralOrder(int[][] matrix) {
        List ans = new ArrayList();
        if (matrix.length == 0)
            return ans;
        int r1 = 0, r2 = matrix.length - 1;
        int c1 = 0, c2 = matrix[0].length - 1;
        while (r1 <= r2 && c1 <= c2) {
            for (int c = c1; c <= c2; c++) ans.add(matrix[r1][c]);
            for (int r = r1 + 1; r <= r2; r++) ans.add(matrix[r][c2]);
            if (r1 < r2 && c1 < c2) {
                for (int c = c2 - 1; c > c1; c--) ans.add(matrix[r2][c]);
                for (int r = r2; r > r1; r--) ans.add(matrix[r][c1]);
            }
            r1++;
            r2--;
            c1++;
            c2--;
        }
        return ans;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(N)，其中 N 是输入矩阵所有元素的个数。因为我们将矩阵中的每个元素都添加进答案里。
- 空间复杂度：O(N)，需要矩阵 ans 存储信息。




## 其他题解
### 1.其它遍历方式
**思路：**
![](https://pic.leetcode-cn.com/5254ec0ff6bec6d954e9abea05d92d8cdcd5136662d2695883bf9d167d8658a9-2019-07-27_124436.jpg)


### 2.优化存储空间
**思路：**

```
class Solution {

    //使用4个int right，down，left，up来记录当前要向这四个方向前进的优先级和前进的步数
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        int row = matrix.length;
        if (row == 0) {
            return result;
        }
        int column = matrix[0].length;

        int size = row * column;
        //当前已经前进的步数
        int currentPosition = 0;
        //当前走到的行index
        int currentRow = 0;
        //当前走到的列index
        int currentColumn = 0;
        //当前走的圈数，right，down，left，up同时为0说明一圈已经走完，round++
        int round = 0;

        int right = column - 1 - round * 2;
        int down = row - 1 - round * 2;
        int left = column - 1 - round * 2;
        int up = row - 2 - round * 2;

        while (currentPosition < size) {
            result.add(matrix[currentRow][currentColumn]);
            //向右前进步数未完，继续向右前进
            if (right > 0) {
                currentColumn++;
                right--;
            } else if (down > 0) {
                //向下前进步数未完，继续向下前进
                currentRow++;
                down--;
            } else if (left > 0) {
                //向左前进步数未完，继续向左前进
                currentColumn--;
                left--;
            } else if (up > 0) {
                //向上前进步数未完，继续向上前进
                currentRow--;

```

**复杂度分析：**
- 时间复杂度：O(N), 一次遍历
- 空间复杂度：O(1)，常数个变量保存前进方向和步数


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/spiral-matrix/solution/luo-xuan-ju-zhen-by-leetcode/)
[heavenrobotxu](https://leetcode-cn.com/problems/spiral-matrix/solution/shi-shi-qian-jin-jie-fa-you-hua-kong-jian-fu-za-du/)***
