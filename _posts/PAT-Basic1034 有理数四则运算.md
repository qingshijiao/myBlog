---
title: 1034 有理数四则运算 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
本题要求编写程序，计算 2 个有理数的和、差、积、商。

### 输入格式：

输入在一行中按照 `a1/b1 a2/b2` 的格式给出两个分数形式的有理数，其中分子和分母全是整型范围内的整数，负号只可能出现在分子前，分母不为 0。

### 输出格式：

分别在 4 行中按照 `有理数1 运算符 有理数2 = 结果` 的格式顺序输出 2 个有理数的和、差、积、商。注意输出的每个有理数必须是该有理数的最简形式
`k a/b`，其中 `k` 是整数部分，`a/b` 是最简分数部分；若为负数，则须加括号；若除法分母为 0，则输出
`Inf`。题目保证正确的输出中没有超过整型范围的整数。

### 输入样例 1：

    
    
    2/3 -4/2
    

### 输出样例 1：

    
    
    2/3 + (-2) = (-1 1/3)
    2/3 - (-2) = 2 2/3
    2/3 * (-2) = (-1 1/3)
    2/3 / (-2) = (-1/3)
    

### 输入样例 2：

    
    
    5/3 0/6
    

### 输出样例 2：

    
    
    1 2/3 + 0 = 1 2/3
    1 2/3 - 0 = 1 2/3
    1 2/3 * 0 = 0
    1 2/3 / 0 = Inf
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <cmath>
using namespace std;
long long a, b, c, d;
long long gcd(long long t1, long long t2) {
    return t2 == 0 ? t1 : gcd(t2, t1 % t2);
}
void func(long long m, long long n) {
    if (m * n == 0) {
        printf("%s", n == 0 ? "Inf" : "0");
        return ;
    }
    bool flag = ((m < 0 && n > 0) || (m > 0 && n < 0));
    m = abs(m); n = abs(n);
    long long x = m / n;
    printf("%s", flag ? "(-" : "");
    if (x != 0) printf("%lld", x);
    if (m % n == 0) {
        if(flag) printf(")");
        return ;
    }
    if (x != 0) printf(" ");
    m = m - x * n;
    long long t = gcd(m, n);
    m = m / t; n = n / t;
    printf("%lld/%lld%s", m, n, flag ? ")" : "");
}
int main() {
    scanf("%lld/%lld %lld/%lld", &a, &b, &c, &d);
    func(a, b); printf(" + "); func(c, d); printf(" = "); func(a * d + b * c, b * d); printf("\n");
    func(a, b); printf(" - "); func(c, d); printf(" = "); func(a * d - b * c, b * d); printf("\n");
    func(a, b); printf(" * "); func(c, d); printf(" = "); func(a * c, b * d); printf("\n");
    func(a, b); printf(" / "); func(c, d); printf(" = "); func(a * d, b * c);
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805287624491008)***
