---
title: 1018 锤子剪刀布 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/xRrOKlZDmgHytqU.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    char a, b;
    int jiawin = 0, yiwin = 0, jia[3] = {0}, yi[3] = {0};
    for(int i = 0; i < n; i++) {
        cin >> a >> b;
        if(a == 'C' && b == 'J'){
            jiawin++;
            jia[1]++;
        } else if(a == 'C' && b == 'B') {
            yiwin++;
            yi[0]++;
        } else if(a == 'J' && b == 'C') {
            yiwin++;
            yi[1]++;
        } else if(a == 'J' && b == 'B') {
            jiawin++;
            jia[2]++;
        } else if(a == 'B' && b == 'C') {
            jiawin++;
            jia[0]++;
        } else if(a == 'B' && b == 'J') {
            yiwin++;
            yi[2]++;
        }
    }
    
    cout << jiawin << " " << (n - jiawin - yiwin) << " " << yiwin << endl;
    cout << yiwin << " " << (n - jiawin - yiwin) << " " << jiawin << endl;
    string str= "BCJ";
    int jiamax = jia[0] >= jia[1]? 0: 1;
    jiamax = jia[jiamax] >= jia[2]? jiamax: 2;
    int yimax = yi[0] >= yi[1]? 0: 1;
    yimax = yi[yimax] >= yi[2]? yimax: 2;
    cout << str[jiamax] << " " << str[yimax];
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805304020025344)***
