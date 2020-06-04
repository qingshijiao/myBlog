---
title: 1062 最简分数 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
一个分数一般写成两个整数相除的形式：N/M，其中 M 不为0。最简分数是指分子和分母没有公约数的分数表示形式。

现给定两个不相等的正分数 N1/M1​​ 和N2/M2，要求你按从小到大的顺序列出它们之间分母为 KKK 的最简分数。

### 输入格式：

输入在一行中按 N/M 的格式给出两个正分数，随后是一个正整数分母 K，其间以空格分隔。题目保证给出的所有整数都不超过 1000。

### 输出格式：

在一行中按 N/M 的格式列出两个给定分数之间分母为 K 的所有最简分数，按从小到大的顺序，其间以 1
个空格分隔。行首尾不得有多余空格。题目保证至少有 1 个输出。

### 输入样例：

    
    
    7/18 13/20 12
    

### 输出样例：

    
    
    5/12 7/12
    

#### Solution

Language: **C++**
```C++
#include <iostream>
using namespace std;
int gcd(int a, int b){
    return b == 0? a: gcd(b, a % b);
}
int main() {
    int n1, m1, n2, m2, k;
    scanf("%d/%d %d/%d %d", &n1, &m1, &n2, &m2, &k);
    double n = (double) n1 * k/ m1;
    double m = (double) n2 * k/ m2;
    if (n > m) {
        swap(n, m);
    }
    int flag = 0;
    for (int i = (int) n + 1; i < m; ++i) {
        if (gcd(k, i) == 1) {
            if (flag == 1) {
                printf(" ");
            }
            printf("%d/%d", i, k);
            flag = 1;
        }
    }
    return 0;
}
```

```c++
#include <iostream>
using namespace std;
int gcd(int a, int b){
    return b == 0 ? a : gcd(b, a % b);
}
int main() {
    int n1, m1, n2, m2, k;
    scanf("%d/%d %d/%d %d", &n1, &m1, &n2, &m2, &k);
    if(n1 * m2 > n2 * m1) {
        swap(n1, n2);
        swap(m1, m2);
    }
    int num = 1;
    bool flag = false;
    while(n1 * k >= m1 * num) num++;
    while(n1 * k < m1 * num && m2 * num < n2 * k) {
        if(gcd(num, k) == 1) {
            printf("%s%d/%d", flag == true ? " " : "", num, k);
            flag = true;
        }
        num++;
    }
    return 0;
}
```
**注意：**
- 并没有说明谁大谁小
- 临界问题

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805268334886912)***
