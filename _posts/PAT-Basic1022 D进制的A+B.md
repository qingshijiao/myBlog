---
title: 1022 D进制的A+B (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/dFgTlntbxfUGm94.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
int main() {
    int a, b, d;
    cin >> a >> b >> d;
    int t = a + b;
    if(t == 0){
        cout << 0;
        return 0;
    }
    int s[100] = {0};
    int i = 0;
    while (t != 0) {
        s[i++] = t % d;
        t /= d;
    }
    for(int j = i - 1; j >= 0; j--) {
        cout << s[j];
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805299301433344)***
