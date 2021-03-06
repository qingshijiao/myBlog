---
title: 1077 互评成绩计算 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
在浙大的计算机专业课中，经常有互评分组报告这个环节。一个组上台介绍自己的工作，其他组在台下为其表现评分。最后这个组的互评成绩是这样计算的：所有其他组的评分中，去掉一个最高分和一个最低分，剩下的分数取平均分记为
G1G_1G​1​​；老师给这个组的评分记为 G2G_2G​2​​。该组得分为
(G1+G2)/2(G_1+G_2)/2(G​1​​+G​2​​)/2，最后结果四舍五入后保留整数分。本题就要求你写个程序帮助老师计算每个组的互评成绩。

### 输入格式：

输入第一行给出两个正整数 NNN（>>> 3）和 MMM，分别是分组数和满分，均不超过 100。随后 NNN 行，每行给出该组得到的 NNN
个分数（均保证为整型范围内的整数），其中第 1 个是老师给出的评分，后面 N−1N-1N−1 个是其他组给的评分。合法的输入应该是 [0,M][0,
M][0,M] 区间内的整数，若不在合法区间内，则该分数须被忽略。题目保证老师的评分都是合法的，并且每个组至少会有 3 个来自同学的合法评分。

### 输出格式：

为每个组输出其最终得分。每个得分占一行。

### 输入样例：

    
    
    6 50
    42 49 49 35 38 41
    36 51 50 28 -1 30
    40 36 41 33 47 49
    30 250 -25 27 45 31
    48 0 0 50 50 1234
    43 41 36 29 42 29
    

### 输出样例：

    
    
    42
    33
    41
    31
    37
    39
    

#### Solution

Language: **C++**
```C++
#include <iostream>
using namespace std;
int main() {
    int n, m, cnt = 0;
    scanf("%d%d", &n, &m);
    double min, max, g1, g2, sco;
    for (int i = 0; i < n; ++i) {
        min = 101.0;
        max = -1.0;
        g1 = 0.0;
        cnt = 0;
        for (int j = 0; j < n; ++j) {
            scanf("%lf", &sco);
            if (j == 0) {
                g2 = sco;
            } else {
                if (sco >= 0 && sco <= m) {
                    min = min > sco? sco: min;
                    max = max < sco? sco: max;
                    g1 += sco;
                    cnt++;
                }
            }
        }
        g1 = (g1 - min -max) / (cnt - 2);
        printf("%d\n", (int) ((g1 + g2) / 2 + 0.5));
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805262303477760)***
