---
title: 1068 万绿丛中一点红 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
对于计算机而言，颜色不过是像素点对应的一个 24 位的数值。现给定一幅分辨率为 M×NM\times NM×N
的画，要求你找出万绿丛中的一点红，即有独一无二颜色的那个像素点，并且该点的颜色与其周围 8 个相邻像素的颜色差充分大。

### 输入格式：

输入第一行给出三个正整数，分别是 MMM 和 NNN（≤\le≤ 1000），即图像的分辨率；以及 TOL，是所求像素点与相邻点的颜色差阈值，色差超过
TOL 的点才被考虑。随后 NNN 行，每行给出 MMM 个像素的颜色值，范围在 [0,224)[0, 2^{24})[0,2​24​​)
内。所有同行数字间用空格或 TAB 分开。

### 输出格式：

在一行中按照 `(x, y): color` 的格式输出所求像素点的位置以及颜色值，其中位置 `x` 和 `y` 分别是该像素在图像矩阵中的列、行编号（从
1 开始编号）。如果这样的点不唯一，则输出 `Not Unique`；如果这样的点不存在，则输出 `Not Exist`。

### 输入样例 1：

    
    
    8 6 200
    0 	 0 	  0 	   0	    0 	     0 	      0        0
    65280 	 65280    65280    16711479 65280    65280    65280    65280
    16711479 65280    65280    65280    16711680 65280    65280    65280
    65280 	 65280    65280    65280    65280    65280    165280   165280
    65280 	 65280 	  16777015 65280    65280    165280   65480    165280
    16777215 16777215 16777215 16777215 16777215 16777215 16777215 16777215
    

### 输出样例 1：

    
    
    (5, 3): 16711680
    

### 输入样例 2：

    
    
    4 5 2
    0 0 0 0
    0 0 3 0
    0 0 0 0
    0 5 0 0
    0 0 0 0
    

### 输出样例 2：

    
    
    Not Unique
    

### 输入样例 3：

    
    
    3 3 5
    1 2 3
    3 4 5
    5 6 7
    

### 输出样例 3：

    
    
    Not Exist
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <vector>
#include <map>
using namespace std;
int m, n, tol;
vector<vector<int>> v;
int dir[8][2] = {{-1, -1}, {-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}, {0, -1}};
bool judge(int i, int j) {
    for (int k = 0; k < 8; k++) {
        int tx = i + dir[k][0];
        int ty = j + dir[k][1];
        if (tx >= 0 && tx < n && ty >= 0 && ty < m && abs(v[i][j] - v[tx][ty]) <= tol) return false;
    }
    return true;
}
int main() {
    int cnt = 0, x = 0, y = 0;
    scanf("%d%d%d", &m, &n, &tol);
    v.resize(n, vector<int>(m));
    map<int, int> mapp;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            scanf("%d", &v[i][j]);
            mapp[v[i][j]]++;
        }
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (mapp[v[i][j]] == 1 && judge(i, j) == true) {
                cnt++;
                x = i + 1;
                y = j + 1;
            }
        }
    }
    if (cnt == 1)
        printf("(%d, %d): %d", y, x, v[x-1][y-1]);
    else if (cnt == 0)
        printf("Not Exist");
    else
        printf("Not Unique");
    return 0;
}
```
```c++
#include <iostream>
#include <vector>
#include <cmath>
#include <map>

using namespace std;

bool isRed(int i, int j, vector<vector<int> > v, int tol){
    if (abs(v[i - 1][j - 1] - v[i][j]) <= tol){ // 左上角
        return false;
    }
    if (abs(v[i][j - 1] - v[i][j]) <= tol){ // 上
        return false;
    }
    if (abs(v[i + 1][j - 1] - v[i][j]) <= tol){ // 右上角
        return false;
    }
    if (abs(v[i + 1][j] - v[i][j]) <= tol){ // 右
        return false;
    }
    if (abs(v[i + 1][j + 1] - v[i][j]) <= tol){ // 右下角
        return false;
    }
    if (abs(v[i][j + 1] - v[i][j]) <= tol){ // 下
        return false;
    }
    if (abs(v[i - 1][j + 1] - v[i][j]) <= tol){ // 左下角
        return false;
    }
    if (abs(v[i - 1][j] - v[i][j]) <= tol){ // 左
        return false;
    }
    return true;
}

vector<vector<int>> v;

int main(){
    int m, n, tol;
    scanf("%d %d %d", &m, &n, &tol);
    // n行m列二维数组
    v.resize(n + 2, vector<int>(m + 2));
    map<int, int> isRepeat;
    for (int i = 1; i <= n; ++i){
        for (int j = 1; j <= m; ++j){
            scanf("%d", &v[i][j]);
            ++isRepeat[v[i][j]];
        }
    }
    int cnt = 0;
    int resI, resJ;
    for (int i = 1; i <= n && cnt < 2; ++i){
        for (int j = 1; j <= m && cnt < 2; ++j){
            if (isRepeat[v[i][j]] == 1 && isRed(i, j, v, tol) == true){ // 只出现过一次
                ++cnt;
                resI = i;
                resJ = j;
            }
        }
    }
    if (cnt == 0){
        printf("Not Exist\n");
    } else if (cnt == 1){
        printf("(%d, %d): %d\n", resJ, resI, v[resI][resJ]);
    } else if (cnt == 2){
        printf("Not Unique\n");
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805265579229184)***
