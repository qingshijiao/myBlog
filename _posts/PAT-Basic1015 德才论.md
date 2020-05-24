---
title: 1015 德才论 (25分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/KrYtUmZB1FXbQfV.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

typedef struct student{
    int id;
    int de;
    int cai;
    int sum;
}stu;

vector<stu> res[5];

bool com(struct student s1, struct student s2) {
    if (s1.sum > s2.sum) {
        return true;
    }
    if(s1.sum == s2.sum) {
        if(s1.de > s2.de) {
            return true;
        }
        if(s1.de == s2.de) {
            return s1.id < s2.id;
        }
        return false;
    }
    return false;
}

int main() {
    int n, l, h, sum = 0;
    cin >> n >> l >> h;
    
    for(int i = 0; i < n; i++){
        stu info;
        cin >> info.id >> info.de >> info.cai;
        info.sum = info.de + info.cai;
        if(info.de < l || info.cai < l){
            continue;
        }
        if(info.de >= h && info.cai >= h) {
            res[0].push_back(info);
        }
        else if(info.de >= h && info.cai < h){
            res[1].push_back(info);
        }
        else if(info.de < h && info.cai < h && info.de >= info.cai){
            res[2].push_back(info);
        }
        else{
            res[3].push_back(info);
        }
        sum++;
    }
    
    cout << sum << endl;
    for(int i = 0; i < 4; i++) {
        sort(res[i].begin(), res[i].end(), com);
    }
    for(int i = 0; i < 4; i++) {
        for(int j = 0; j < res[i].size(); j++){
            printf("%d %d %d\n", res[i][j].id, res[i][j].de, res[i][j].cai);
        }
    }
    
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805307551629312)***
