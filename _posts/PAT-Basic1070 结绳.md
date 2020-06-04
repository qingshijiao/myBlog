---
title: 1070 结绳 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
给定一段一段的绳子，你需要把它们串成一条绳。每次串连的时候，是把两段绳子对折，再如下图所示套接在一起。这样得到的绳子又被当成是另一段绳子，可以再次对折去跟另一段绳子串连。每次串连后，原来两段绳子的长度就会减半。

![rope.jpg](https://images.ptausercontent.com/46293e57-aa0e-414b-b5c3-7c4b2d5201e2.jpg)

给定 NNN 段绳子的长度，你需要找出它们能串成的绳子的最大长度。

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例第 1 行给出正整数 NNN (2≤N≤1042 \le N \le 10^42≤N≤10​4​​)；第 2
行给出 NNN 个正整数，即原始绳段的长度，数字间以空格分隔。所有整数都不超过10410^410​4​​。

### 输出格式：

在一行中输出能够串成的绳子的最大长度。结果向下取整，即取为不超过最大长度的最近整数。

### 输入样例：

    
    
    8
    10 15 12 3 4 13 1 15
    

### 输出样例：

    
    
    14
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int n;
    scanf("%d", &n);
    double k[n], sum;
    for (int i = 0; i < n; i++) {
        scanf("%lf", &k[i]);
    }
    sort(k, k + n);
    sum = k[0];
    for (int i = 0; i < n; i++) {
        sum = sum / 2 + k[i] / 2;
    }
    printf("%d", (int) sum);
    return 0;
}
```

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int n;
    scanf("%d", &n);
    double k[n], sum;
    for (int i = 0; i < n; i++) {
        scanf("%lf", &k[i]);
    }
    sort(k, k + n);
    sum = k[0];
    for (int i = 0; i < n; i++) {
        sum = sum / 2 + k[i] / 2;
    }
    printf("%d", (int) sum);
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805264706813952)***
