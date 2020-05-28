---
title: 1037 在霍格沃茨找零钱 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
如果你是哈利·波特迷，你会知道魔法世界有它自己的货币系统 ——
就如海格告诉哈利的：“十七个银西可(Sickle)兑一个加隆(Galleon)，二十九个纳特(Knut)兑一个西可，很容易。”现在，给定哈利应付的价钱
PPP 和他实付的钱 AAA，你的任务是写一个程序来计算他应该被找的零钱。

### 输入格式：

输入在 1 行中分别给出 P 和 A，格式为 `Galleon.Sickle.Knut`，其间用 1 个空格分隔。这里 `Galleon` 是
[0, 10^7​​] 区间内的整数，`Sickle` 是 [0, 17) 区间内的整数，`Knut` 是 [0, 29) 区间内的整数。

### 输出格式：

在一行中用与输入同样的格式输出哈利应该被找的零钱。如果他没带够钱，那么输出的应该是负数。

### 输入样例 1：

    
    
    10.16.27 14.1.28
    

### 输出样例 1：

    
    
    3.2.1
    

### 输入样例 2：

    
    
    14.1.28 10.16.27
    

### 输出样例 2：

    
    
    -3.2.1
    

#### Solution

Language: **C++**
```C++
#include <iostream>

using namespace std;
int main() {
    int a[3], b[3], res[3];
    scanf("%d.%d.%d %d.%d.%d", &a[0], &a[1], &a[2], &b[0], &b[1], &b[2]);
    int c = 0;
    int temp = (b[0] * 17 * 29 + b[1] * 29 + b[2]) - (a[0] * 17 * 29 + a[1] * 29 + a[2]);
    if (temp < 0) {
        cout << "-";
    }
    temp = abs(temp);
    res[0] = temp / 29 / 17;
    res[1] = temp / 29 % 17;
    res[2] = temp % 29;
    
    cout << res[0] << "." << res[1] << "." << res[2];
    return 0;
}
```

```c++
#include <iostream>
using namespace std;
int main() {
    int a, b ,c, m, n, t, x, y, z;
    scanf("%d.%d.%d %d.%d.%d",&a, &b, &c, &m, &n, &t);
    if (a > m || (a == m && b > n) || (a == m && b == n && c > t)) {
        swap(a, m); swap(b, n); swap(c, t);
        printf("-");        
    }
    z = t < c ? t - c + 29 : t - c;
    n = t < c ? n - 1 : n;
    y = n < b ? n - b + 17 : n - b;
    x = n < b ? m - a - 1 : m - a;
    printf("%d.%d.%d", x, y, z);
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805284923359232)***
