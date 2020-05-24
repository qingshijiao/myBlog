---
title: 1002 写出这个数 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
1002 写出这个数 (20分)
读入一个正整数 n，计算其各位数字之和，用汉语拼音写出和的每一位数字。

输入格式：
每个测试输入包含 1 个测试用例，即给出自然数 n 的值。这里保证 n 小于 10
​100
​​ 。

输出格式：
在一行内输出 n 的各位数字之和的每一位，拼音数字间有 1 空格，但一行中最后一个拼音数字后没有空格。

输入样例：
1234567890987654321123456789
输出样例：
yi san wu


#### Solution

Language: **C++**

```C++
#include<iostream>
#include<string>
using namespace std;
int main()
{
    string pinyin[10]={"ling","yi","er","san","si","wu","liu","qi","ba","jiu"};
    string a;
    cin >> a;
    int sum=0;
    int len=a.length();
    for(int i=0;i<len;i++)
    {
        sum+=a[i]-'0';
    }
    string s=to_string(sum);
    int len1=s.length();
    for(int i=0;i<len1;i++)
    {
        cout<<pinyin[s[i]-'0'];
        if(i<len1-1) cout <<" ";
    }
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805324509200384)***
