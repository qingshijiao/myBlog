---
title: 51. N 皇后（N-Queens）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/8-queens.png)
上图为 8 皇后问题的一种解法。
给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

示例:
```
输入: 4
输出: [
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```



# 题解

## 官方题解
### 1.约束编程 + 回溯算法
**思路：**
![](https://pic.leetcode-cn.com/e67ed217a00038ed292ae8cb89c1a8492c7a49e33ec17f633f41c4ece77d6c2c-51_pic.png)
```
class Solution {
  public List<List<String>> solveNQueens(int n) {
        int[] col=new int[n];//棋子放置位置
        int[] row=new int[n];
        int[] dig=new int[2*n-1];
        int[] hill=new int[2*n-1];
        List<List<String>> answer=new ArrayList<>();
        List<List<String>> a=place(n,0,row,dig,hill,col,answer);
        return a;

    }
    List<List<String>>  place (int n,int m,int[]row,int[]dig,int [] hill,int[] col,List<List<String>> answer){
        if(n==m) {
            List<String> ans=new ArrayList<String>();

            for (int i=0;i<n;i++){
                StringBuilder sol=new StringBuilder();
                for(int j=0;j<col[i];j++){
                    sol.append('.');
                }
                sol.append('Q');
                for(int j=(col[i]+1);j<n;j++){
                    sol.append('.');
                }
                String solu=sol.toString();
                ans.add(solu);
            }
            answer.add(ans);
        }
        else{
            for(int i=0;i<n;i++) {
                int res=row[i]+dig[i+m]+hill[i-m+n-1];
                if(res==0){
                    col[m]=i;
                    row[i]=1;
                    dig[i+m]=1;
                    hill[i-m+n-1]=1;
                    place(n,(m+1),row,dig,hill,col,answer);
                    col[m]=0;
                    row[i]=0;
                    dig[i+m]=0;
                    hill[i-m+n-1]=0;
                }

            }
        }
        return answer;

    }

}


```

## 其他题解
### 1.位运算
**思路：**
```
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        int cons = (1 << n) - 1;
        func(res, new ArrayList(), n, 0, 0, 0, cons, n);
        return res;
    }

    public void func(List<List<String>> res, List<String> list, int n,
        int shu, int pie, int na, int cons, int len){
        if(n == 0){
            res.add(new ArrayList(list));
            return;
        }
        int bit = ~(shu | pie | na) & cons;
        char[] ch = new char[len];
        for(int i = 0; i < len; i++) ch[i] = '.';
        int idx = 0;
        while(bit != 0){
            int temp = bit & -bit;
            for(; idx < len; idx++){
                if(1 << idx == temp){
                    ch[idx] = 'Q';
                    break;
                }
            }
            list.add(new String(ch));
            func(res, list, n - 1, shu | temp, (pie | temp) << 1,
                (na | temp) >> 1, cons, len);
            bit ^= temp;
            ch[idx] = '.';
            list.remove(list.size() - 1);
        }
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/count-and-say/)***
