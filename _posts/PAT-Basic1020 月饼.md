---
title: 1020 月饼 (25分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/aSOtYvd1HbqCyXn.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
struct mooncake{
    float mount, price, unit;
};
int cmp(mooncake a, mooncake b) {
    return a.unit > b.unit;
}
int main() {
    int n, d;
    cin >> n >> d;
    vector<mooncake> m(n);
    for(int i = 0; i < n; i++) cin >> m[i].mount;
    for(int i = 0; i < n; i++) cin >> m[i].price;
    for(int i = 0; i < n; i++) m[i].unit =  m[i].price / m[i].mount;
    sort(m.begin(), m.end(), cmp);
    float res = 0.0f;
    for(int i = 0; i < n; i++){
        if(m[i].mount >= d) {
            res += m[i].unit * d;
            break;
        } else {
            res += m[i].mount * m[i].unit;
        }
        d -= m[i].mount;
    }
    printf("%.2f", res);
    
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805301562163200)***
