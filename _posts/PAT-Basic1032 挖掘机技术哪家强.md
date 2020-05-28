---
title: 1032 挖掘机技术哪家强 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
为了用事实说明挖掘机技术到底哪家强，PAT 组织了一场挖掘机技能大赛。现请你根据比赛结果统计出技术最强的那个学校。

### 输入格式：

输入在第 1 行给出不超过 10^5 的正整数 N，即参赛人数。随后 N
行，每行给出一位参赛者的信息和成绩，包括其所代表的学校的编号（从 1 开始连续编号）、及其比赛成绩（百分制），中间以空格分隔。

### 输出格式：

在一行中给出总得分最高的学校的编号、及其总分，中间以空格分隔。题目保证答案唯一，没有并列。

### 输入样例：

    
    
    6
    3 65
    2 80
    1 100
    2 70
    3 40
    3 0
    

### 输出样例：

    
    
    2 150
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <vector>
using namespace std;
int main() {
    int N;
    cin >> N;
    vector<int> a(N + 1);
    int num, score;
    for (int i = 0; i < N; i++) {
        cin >> num >> score;
        a[num] += score;
    }
    int max = a[1], t = 1;
    for (int i = 2; i <= N; i++) {
        if (max < a[i]) {
            max = a[i];
            t = i;
        }
    }
    cout << t << " " << max;
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805289432236032)***
