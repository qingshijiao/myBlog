---
title: 1065 单身狗 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
“单身狗”是中文对于单身人士的一种爱称。本题请你从上万人的大型派对中找出落单的客人，以便给予特殊关爱。

### 输入格式：

输入第一行给出一个正整数 N（≤\le≤ 50 000），是已知夫妻/伴侣的对数；随后 N 行，每行给出一对夫妻/伴侣——为方便起见，每人对应一个 ID
号，为 5 位数字（从 00000 到 99999），ID 间以空格分隔；之后给出一个正整数 M（≤\le≤ 10
000），为参加派对的总人数；随后一行给出这 M 位客人的 ID，以空格分隔。题目保证无人重婚或脚踩两条船。

### 输出格式：

首先第一行输出落单客人的总人数；随后第二行按 ID 递增顺序列出落单的客人。ID 间用 1 个空格分隔，行的首尾不得有多余空格。

### 输入样例：

    
    
    3
    11111 22222
    33333 44444
    55555 66666
    7
    55555 44444 10000 88888 22222 11111 23333
    

### 输出样例：

    
    
    5
    10000 23333 44444 55555 88888
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <map>
using namespace std;
int main() {
    int n, m, k1, k2, k;
    int par[100005] = {0};
    scanf("%d", &n);
    map<int, int> hw;
    for (int i = 0; i < n; ++i) {
        scanf("%d %d", &k1, &k2);
        hw[k1] = k2;
        hw[k2] = k1;
    }
    scanf("%d", &m);
    for (int i = 0; i < m; ++i) {
        scanf("%d", &k);
        par[k] = 1;
    }
    for (int i = 0; i < 100005; ++i) {
        if (hw[i] != 0 && par[i] != 0 && par[hw[i]] != 0) {
            par[i] = 0;
            par[hw[i]] = 0;
            m -= 2;
        }
    }
    printf("%d\n", m);
    int flag = 0;
    for (int i = 0; i < 100005; ++i) {
        if (par[i] == 1) {
            printf("%s%05d", flag == 0? "": " ", i);
            flag = 1;
        }

    }
    return 0;
}
```
```c++
#include <iostream>
#include <vector>
#include <set>
using namespace std;
int main() {
    int n, a, b, m;
    scanf("%d", &n);
    vector<int> couple(100000, -1);
    for (int i = 0; i < n; i++) {
        scanf("%d%d", &a, &b);
        couple[a] = b;
        couple[b] = a;
    }
    scanf("%d", &m);
    vector<int> guest(m), isExist(100000);
    for (int i = 0; i < m; i++) {
        scanf("%d", &guest[i]);
        if (couple[guest[i]] != -1)
            isExist[couple[guest[i]]] = 1;
    }
    set<int> s;
    for (int i = 0; i < m; i++) {
        if (!isExist[guest[i]])
            s.insert(guest[i]);
    }
    printf("%d\n", s.size());
    for (auto it = s.begin(); it != s.end(); it++) {
        if (it != s.begin()) printf(" ");
        printf("%05d", *it);
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805266942377984)***
