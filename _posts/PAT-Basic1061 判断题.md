---
title: 1061 判断题 (15分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
判断题的评判很简单，本题就要求你写个简单的程序帮助老师判题并统计学生们判断题的得分。

### 输入格式：

输入在第一行给出两个不超过 100 的正整数 N 和 M，分别是学生人数和判断题数量。第二行给出 M 个不超过 5
的正整数，是每道题的满分值。第三行给出每道题对应的正确答案，0 代表“非”，1 代表“是”。随后 N 行，每行给出一个学生的解答。数字间均以空格分隔。

### 输出格式：

按照输入的顺序输出每个学生的得分，每个分数占一行。

### 输入样例：

    
    
    3 6
    2 1 3 3 4 5
    0 0 1 0 1 1
    0 1 1 0 0 1
    1 0 1 0 1 0
    1 1 0 0 1 1
    

### 输出样例：

    
    
    13
    11
    12
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main() {
    int n, m;
    cin >> n >> m;
    int score[m], tAns[m];
    for (int i = 0; i < m; ++i) {
        cin >> score[i];
    }
    for (int i = 0; i < m; ++i) {
        cin >> tAns[i];
    }
    int res, a;
    for (int i = 0; i < n; ++i) {
        res = 0;
        for (int i = 0; i < m; ++i) {
            cin >> a;
            if (a == tAns[i]){
                res += score[i];
            }
        }
        cout << res << endl;
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805268817231872)***
