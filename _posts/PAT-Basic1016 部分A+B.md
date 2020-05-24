---
title: 1016 部分A+B (15分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/wOuSJgd8QjnVN7X.png)

#### Solution

Language: **C++**

```C++
#include <iostream>

using namespace std;

int main() {
    string a, b;
    int da, db, pa = 0, pb = 0;
    cin >> a >> da >> b >> db;
    int alen = a.length();
    int blen = b.length();
    for(int i = 0; i < alen; i++){
        if(a[i] - '0' == da) {
            pa *= 10;
            pa += da;
        }
    }
    for(int j = 0; j < blen; j++){
        if(b[j] - '0' == db) {
            pb *= 10;
            pb += db;
        }
    }
    
    cout << (pa + pb);
    
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805306310115328)***
