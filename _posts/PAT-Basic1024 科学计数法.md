---
title: 1024 科学计数法 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/lb5nUq4WD2Fc9Ie.png)


#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
int main() {
    string a;
    cin >> a;
    int i = 0;
    while (a[i] != 'E') i++;
    string t = a.substr(1, i - 1);
    int n = stoi(a.substr(i + 1));
    if(a[0] == '-'){
        cout << '-';
    }
    if(n < 0) {
        cout << "0.";
        for(int j = 0; j < abs(n) - 1; j++) cout << '0';
        for(int j = 0; j < t.length(); j++) {
            if(t[j] != '.') {
                cout << t[j];
            }
        }
    } else {
        cout << t[0];
        int j = 2, cnt = 0;
        for (; j < t.length() && cnt < n; j++, cnt++) {
            cout << t[j];
        }
        if (j < t.length()) {
            cout << '.';
            while(j < t.length()) {
                cout << t[j++];
            }
        } else {
            while(cnt < n) {
                cout << '0';
                cnt++;
            }
        }
    }
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805297229447168)***
