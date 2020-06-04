---
title: 1060 爱丁顿数 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
英国天文学家爱丁顿很喜欢骑车。据说他为了炫耀自己的骑车功力，还定义了一个“爱丁顿数” EEE ，即满足有 EEE 天骑车超过 EEE 英里的最大整数
EEE。据说爱丁顿自己的 EEE 等于87。

现给定某人 NNN 天的骑车距离，请你算出对应的爱丁顿数 EEE（≤N\le N≤N）。

### 输入格式：

输入第一行给出一个正整数 NNN (≤105\le 10^5≤10​5​​)，即连续骑车的天数；第二行给出 NNN 个非负整数，代表每天的骑车距离。

### 输出格式：

在一行中给出 NNN 天的爱丁顿数。

### 输入样例：

    
    
    10
    6 7 6 9 3 10 8 2 7 8
    

### 输出样例：

    
    
    6
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
bool cmp(int x1, int x2) {
    return x1 > x2;
}
int main() {
    int n, ans = 0;
    scanf("%d", &n);
    vector<int> v(n);
    for (int i = 0; i < n; ++i) {
        scanf("%d", &v[i]);
    }
    sort(v.begin(), v.end(), cmp);
    if (v[n - 1] > n) {
        printf("%d", n);
    } else {
        for (int i = 0; i < n; ++i) {
            if (v[i] <= i + 1) {
                ans = i;
                break;
            }
        }
        printf("%d", ans);
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805269312159744)***
