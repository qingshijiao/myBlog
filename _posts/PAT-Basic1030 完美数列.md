---
title: 1030 完美数列 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
给定一个正整数数列，和正整数 p，设这个数列中的最大值是 M，最小值是 m，如果 M≤mp，则称这个数列是完美数列。

现在给定参数 p 和一些正整数，请你从中选择尽可能多的数构成一个完美数列。

### 输入格式：

输入第一行给出两个正整数 NNN 和 ppp，其中 N（≤ 10^5​​）是输入的正整数的个数，p（≤10^9）是给定的参数。第二行给出 N 个正整数，每个数不超过 10^9​​。

### 输出格式：

在一行中输出最多可以选择多少个数可以用它们组成一个完美数列。

### 输入样例：

    
    
    10 8
    2 3 20 4 5 1 6 7 8 9
    

### 输出样例：

    
    
    8
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int n;
    long long p;
    cin >> n >> p;
    int num[n];
    for (int i = 0; i < n; i++) {
        cin >> num[i];
    }
    sort(num, num + n);
    int res = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i + res; j < n; j++) {
            if (num[j] <= num[i] * p) {
                res++;
            } else {
                break;
            }
        }
    }
    cout << res;
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805291311284224)***
