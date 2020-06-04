---
title: 1080 MOOC期终成绩 (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
对于在中国大学MOOC（<http://www.icourse163.org/>
）学习“数据结构”课程的学生，想要获得一张合格证书，必须首先获得不少于200分的在线编程作业分，然后总评获得不少于60分（满分100）。总评成绩的计算公式为
G=(Gmid−term×40%+Gfinal×60%)，如果 Gmid−term>Gfinal​​；否则总评 G 就是 G​final​​。这里 G​mid−term​​ 和 G​final​​ 分别为学生的期中和期末成绩。

现在的问题是，每次考试都产生一张独立的成绩单。本题就请你编写程序，把不同的成绩单合为一张。

### 输入格式：

输入在第一行给出3个整数，分别是 P（做了在线编程作业的学生数）、M（参加了期中考试的学生数）、N（参加了期末考试的学生数）。每个数都不超过10000。

接下来有三块输入。第一块包含 P 个在线编程成绩 G​p​​；第二块包含 M 个期中考试成绩 G​mid−term​​；第三块包含 N 个期末考试成绩 }G​final​​。每个成绩占一行，格式为：`学生学号
分数`。其中`学生学号`为不超过20个字符的英文字母和数字；`分数`是非负整数（编程总分最高为900分，期中和期末的最高分为100分）。

### 输出格式：

打印出获得合格证书的学生名单。每个学生占一行，格式为：

`学生学号` Gp​​ Gmid−term​​ Gfinal G

如果有的成绩不存在（例如某人没参加期中考试），则在相应的位置输出“−1”。输出顺序为按照总评分数（四舍五入精确到整数）递减。若有并列，则按学号递增。题目保证学号没有重复，且至少存在1个合格的学生。

### 输入样例：

    
    
    6 6 7
    01234 880
    a1903 199
    ydjh2 200
    wehu8 300
    dx86w 220
    missing 400
    ydhfu77 99
    wehu8 55
    ydjh2 98
    dx86w 88
    a1903 86
    01234 39
    ydhfu77 88
    a1903 66
    01234 58
    wehu8 84
    ydjh2 82
    missing 99
    dx86w 81
    

### 输出样例：

    
    
    missing 400 -1 99 99
    ydjh2 200 98 82 88
    dx86w 220 88 81 84
    wehu8 300 55 84 84
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
#include <vector>
#include <map>
using namespace std;
struct grade {
	int g1, g2, g3, g4;
    grade () {
        g2 = g3 = g4 = -1;
    }
};
bool cmp(pair<string, grade> &p1, pair<string, grade> &p2) {
	if (p1.second.g4 == p2.second.g4) {
		return p1.first < p2.first;
	} else {
		return p1.second.g4 > p2.second.g4;
	}
}
int main() {
    int p, m, n, sctemp;
    scanf("%d%d%d", &p, &m, &n);
    map<string, grade> mapp;
    string ntemp;
    for (int i = 0; i < p; ++i) {
        cin >> ntemp >> sctemp;
        mapp[ntemp].g1 = sctemp;
    }
    for (int i = 0; i < m; ++i) {
        cin >> ntemp >> sctemp;
        mapp[ntemp].g2 = sctemp;
    }
    for (int i = 0; i < n; ++i) {
        cin >> ntemp >> sctemp;
        mapp[ntemp].g3 = sctemp;
        if (mapp[ntemp].g2 > mapp[ntemp].g3) {
            mapp[ntemp].g4 = (int) ((double) mapp[ntemp].g2 * 0.4 + (double) mapp[ntemp].g3 * 0.6 + 0.5);
        } else {
            mapp[ntemp].g4 = mapp[ntemp].g3;
        }
    }
    vector<pair<string, grade>> v(mapp.begin(), mapp.end());
    sort(v.begin(), v.end(), cmp);
    vector<pair<string, grade>>::iterator iter;
    for (iter = v.begin(); iter != v.end(); ++iter) {
    	if (iter->second.g1 < 200 || iter->second.g4 < 60) {
    		continue;
		}
        cout << iter->first;
        printf(" %d %d %d %d\n", iter->second.g1, iter->second.g2, iter->second.g3, iter->second.g4);
    }
    return 0;
}
```
```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <map>
using namespace std;
struct node {
    string name;
    int gp, gm, gf, g;
};
bool cmp(node a, node b) {
    return a.g != b.g ? a.g > b.g : a.name < b.name;
}
map<string, int> idx;
int main() {
    int p, m, n, score, cnt = 1;
    cin >> p >> m >> n;
    vector<node> v, ans;
    string s;
    for (int i = 0; i < p; i++) {
        cin >> s >> score;
        if (score >= 200) {
            v.push_back(node{s, score, -1, -1, 0});
            idx[s] = cnt++;
        }
    }
    for (int i = 0; i < m; i++) {
        cin >> s >> score;
        if (idx[s] != 0) v[idx[s] - 1].gm = score;
    }
    for (int i = 0; i < n; i++) {
        cin >> s >> score;
        if (idx[s] != 0) {
            int temp = idx[s] - 1;
            v[temp].gf = v[temp].g = score;
            if (v[temp].gm > v[temp].gf) v[temp].g = int(v[temp].gm * 0.4 + v[temp].gf * 0.6 + 0.5);
        }
    }
    for (int i = 0; i < v.size(); i++)
        if (v[i].g >= 60) ans.push_back(v[i]);
    sort(ans.begin(), ans.end(), cmp);
    for (int i = 0; i < ans.size(); i++)
        printf("%s %d %d %d %d\n", ans[i].name.c_str(), ans[i].gp, ans[i].gm, ans[i].gf, ans[i].g);
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805261493977088)***
