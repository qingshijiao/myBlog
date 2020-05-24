---
title: 1023 组个最小数 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/VxytlaL4DYeW2Qz.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int n, flag = 0, num[10] = {0};
    for(int i = 0; i < 10; i++){
        cin >> n;
        num[i] = n;
        if(i != 0  && n != 0 && flag == 0){
            cout << i;
            num[i]--;
            flag = 1;
        }
    }
    
    for(int i = 0; i < 10; i++) {
        for(int j = 0; j < num[i]; j++) {
            cout << i;
        }
    }
    return 0;
}
```

```C++
#include <iostream>
using namespace std;
int main() {
    int a[10], t;
    for (int i = 0; i < 10; i++)
        cin >> a[i];
    for (int i = 1; i < 10; i++) {
        if (a[i] != 0) {
            cout << i;
            t = i;
            break;
        }
    }
    for (int i = 0; i < a[0]; i++) cout << 0;
    for (int i = 0; i < a[t] - 1; i++) cout << t;
    for (int i = t + 1; i < 10; i++)
        for (int k = 0; k < a[i]; k++)
            cout << i;
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805298269634560)***
