---
title: 1011 A+B 和 C (15分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/23/S6cn2VWA8PQOifU.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
int main() {
    int n;
    long long int a, b, c;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a >> b >> c;
        if (a - c > -b){
            cout << "Case #" << i + 1 << ": true" << endl;
        }
        else{
            cout << "Case #" << i + 1 << ": false" << endl;
        }
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805312417021952)***
