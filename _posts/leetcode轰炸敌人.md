---
title: 361.轰炸敌人 (Bomb Enemy)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a 2D grid, each cell is either a wall 'W', an enemy 'E' or empty '0' (the number zero), return the maximum enemies you can kill using one bomb.
The bomb kills all the enemies in the same row and column from the planted point until it hits the wall since the wall is too strong to be destroyed.
Note that you can only put the bomb at an empty cell.

Example:
```
For the given grid

0 E 0 0
E 0 W E
0 E 0 0

return 3. (Placing a bomb at (1,1) kills 3 enemies)
```

#### Solution

Language: **c++**

```c++
class Solution {
public:
    int maxKilledEnemies(vector<vector<char>>& grid) {
        if(grid.size() == 0 || grid[0].size() == 0) {
            return 0;
        }
        int row = grid.size(), col = grid[0].size(), rowHits, colHits[col], ans = 0;
        for(int i = 0; i < row; ++i) {
            for(int j = 0; j < col; ++j) {
                if(i == 0 || grid[i-1][j]=='W') {   // update colHits[j] only if the row starts from 0 or the up element is 'W'
                    colHits[j] = 0;
                    for(int k = i; k < row && grid[k][j]!='W'; ++k) {
                        colHits[j] += (grid[k][j] == 'E');
                    }
                }
                if(j == 0 || grid[i][j-1] == 'W') { // update rowHits only if the col start from 0 or the left element is 'W'
                    rowHits = 0;
                    for(int k = j; k < col && grid[i][k]!='W'; ++k) {
                        rowHits += (grid[i][k] == 'E');
                    }
                }
                if(grid[i][j] == '0') {
                    ans = max(ans, colHits[j] + rowHits);
                }
            }
        }
        return ans;
    }
};
```
---
***参考:
[magicbean2](https://blog.csdn.net/magicbean2/article/details/77266303)***
