---
title: 1013 数素数 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/23/dzPFKeGqbgODl2R.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
bool isPrime(int n){
    for(int i = 2; i * i <= n; i++){
        if(n % i == 0){
            return false;
        }
    }
    return true;
}
int main() {
    int m, n, cou = 1;
    cin >> m >> n;
    if(m <= 1) {
        cout << "2";
        if(n >= 2){
           cout << " "; 
        }
    }
    for (int i = 3; cou <= n; i += 2) {
        if (isPrime(i)){
            cou++;
            if(cou >= m && cou <= n){
                cout << i;
                if((cou - m + 1) % 10 == 0){
                    cout << endl;
                }
                if((cou - m + 1) % 10 != 0 && cou != n){
                    cout << " ";
                }
            }
        }
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805309963354112)***
