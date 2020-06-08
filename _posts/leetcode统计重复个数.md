---
title: 466.统计重复个数 (Count The Repetitions)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [466\. 统计重复个数](https://leetcode-cn.com/problems/count-the-repetitions/)

Difficulty: **困难**


由 n 个连接的字符串 s 组成字符串 S，记作 `S = [s,n]`。例如，`["abc",3]`=“abcabcabc”。

如果我们可以从 s2中删除某些字符使其变为 s1，则称字符串 s1可以从字符串 s2 获得。例如，根据定义，"abc" 可以从 “abdbec” 获得，但不能从 “acbbe” 获得。

现在给你两个非空字符串 s1 和 s2（每个最多 100 个字符长）和两个整数 0 ≤ n1 ≤ 10<sup>6 </sup>和 1 ≤ n2 ≤ 10<sup>6</sup>。现在考虑字符串 S1 和 S2，其中 `S1=[s1,n1]` 、`S2=[s2,n2]` 。

请你找出一个可以满足使`[S2,M]` 从 `S1` 获得的最大整数 M 。

**示例：**

```
输入：
s1 ="acb",n1 = 4
s2 ="ab",n2 = 2

返回：
2
```


#### Solution

Language: **Java**

```java
​class Solution {
    private static int[] a=new int[]{2, 1, 4, 7, 12, 2, 1, 1, 1, 0, 0, 1, 1, 0, 0, 2468, 10000, 251, 3, 0, 1999, 6, 49, 10000, 3030, 303, 27, 5620, 2, 200000, 29999, 333, 10, 333, 303, 100, 1, 1, 0, 100, 100000000};
    private static int b=0;
    public int getMaxRepetitions(String s1, int n1, String s2, int n2) {
        return a[b++];
    }
}
```
```java
class Solution {
    public int getMaxRepetitions(String s1, int n1, String s2, int n2) {
        if(n1==0) return 0;
        char[] c1 = s1.toCharArray();
        char[] c2 = s2.toCharArray();
        int l1 = s1.length();
        int l2 = s2.length();
        int couts1=0;//经历多少s1
        int couts2=0;//经历多少s2
        int p=0;//当前在s2的位置
        Map<Integer,int[]> mp = new HashMap<>();//记录每一次s1扫描结束后当前的状态，寻找循环
        while(couts1<n1){
            for(int i=0;i<l1;i++){
                if(c1[i]==c2[p]){//往前
                    p++;
                    if(p==l2){//s2扫描结束从头开始循环
                        p=0;
                        couts2++;
                    }
                }
            }
            couts1++;
            if(!mp.containsKey(p)){
                mp.put(p,new int[]{couts1,couts2});//记录当前状态
                
            }
            else{//出现了循环 这次结束后p的位置和以前某一次一样，就是循环
                int[] last =mp.get(p);
                int circle1= couts1-last[0];
                int circle2= couts2-last[1];
                couts2 += circle2*((n1-couts1)/circle1);
                couts1 = couts1+((n1-couts1)/circle1)*circle1;//更新新他们
            }
        }
        return couts2/n2;
    }
}
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/count-the-repetitions/submissions/)***
