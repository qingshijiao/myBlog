---
title: 1055 集体照 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
拍集体照时队形很重要，这里对给定的 NNN 个人 KKK 排的队形设计排队规则如下：

  * 每排人数为 N/KN/KN/K（向下取整），多出来的人全部站在最后一排；

  * 后排所有人的个子都不比前排任何人矮；

  * 每排中最高者站中间（中间位置为 m/2+1m/2+1m/2+1，其中 mmm 为该排人数，除法向下取整）；

  * 每排其他人以中间人为轴，按身高非增序，先右后左交替入队站在中间人的两侧（例如5人身高为190、188、186、175、170，则队形为175、188、190、186、170。这里假设你面对拍照者，所以你的左边是中间人的右边）；

  * 若多人身高相同，则按名字的字典序升序排列。这里保证无重名。

现给定一组拍照人，请编写程序输出他们的队形。

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例第 1 行给出两个正整数 NNN（≤104\le 10^4≤10​4​​，总人数）和 KKK（≤10\le
10≤10，总排数）。随后 NNN 行，每行给出一个人的名字（不包含空格、长度不超过 8 个英文字母）和身高（[30, 300] 区间内的整数）。

### 输出格式：

输出拍照的队形。即K排人名，其间以空格分隔，行末不得有多余空格。注意：假设你面对拍照者，后排的人输出在上方，前排输出在下方。

### 输入样例：

    
    
    10 3
    Tom 188
    Mike 170
    Eva 168
    Tim 160
    Joe 190
    Ann 168
    Bob 175
    Nick 186
    Amy 160
    John 159
    

### 输出样例：

    
    
    Bob Tom Joe Nick
    Ann Mike Eva
    Tim Amy John
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
struct people{
    string name;
    int height;
};
bool cmp(struct people p1, struct people p2) {
    return p1.height != p2.height? p1.height < p2.height: p1.name > p2.name;
}
int main() {
    int n, k;
    cin >> n >> k;
    vector<people> v(n);
    for (int i = 0; i < n; ++i) {
        cin >> v[i].name >> v[i].height;
    }
    sort(v.begin(), v.end(), cmp);
    int row = k, num = 0, left = n;
    while (row) {
        if (row == k) {
            num = n / k + n % k;
        } else {
            num = n / k;
        }
        int j = num % 2 == 0? left - num: left - num + 1;
        for (; j < left; j += 2) {
            cout << v[j].name << " ";
        }
        j = left - 1;
        for (; j >= left - num; j -= 2) {
        	if(j != left - 1) {
        		cout << " ";
			}
            cout << v[j].name;
        }
        if (row != 1) {
            printf("\n");
        }
        
        left -= num;
        row--;
    }
    return 0;
}
```

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
struct node {
    string name;
    int height;
};
int cmp(struct node a, struct node b) {
    return a.height != b.height ? a.height > b.height : a.name < b.name;
}
int main() {
    int n, k, m;
    cin >> n >> k;
    vector<node> stu(n);
    for(int i = 0; i < n; i++) {
        cin >> stu[i].name >> stu[i].height;
    }
    sort(stu.begin(), stu.end(), cmp);
    int t = 0, row = k;
    while(row) {
        if(row == k)
            m = n - n / k * (k - 1);
        else
            m = n / k;
        vector<string> ans(m);
        ans[m / 2] = stu[t].name;
        // 左边一列
        int j = m / 2 - 1;
        for(int i = t + 1; i < t + m; i = i + 2)
            ans[j--] = stu[i].name;
        // 右边一列
        j = m / 2 + 1;
        for(int i = t + 2; i < t + m; i = i + 2)
            ans[j++] = stu[i].name;
        // 输出当前排
        cout << ans[0];
        for(int i = 1; i < m; i++)
            cout << " " << ans[i];
        cout << endl;
        t = t + m;
        row--;
    }
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805272021680128)***
