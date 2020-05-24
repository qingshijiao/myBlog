---
title: 1007 素数对猜想 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/23/cYBJvEXFNSx7j52.png)

#### Solution

Language: **C++**

```C++
#include <iostream>

using namespace std;

bool isQ(int n) {
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0){
            return false;
        }
    }
    return true;
}

int main() {
    int n, count = 0, pre = 2;
    cin >> n;
    for (int i = 3; i <= n; i += 2) {
        if (isQ(i)){
            if(i - pre == 2) {
                ++count;
            }
            pre = i;
        }
    }
    cout << count;
    
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805317546655744)***
