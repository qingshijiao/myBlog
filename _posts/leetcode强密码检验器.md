---
title: 420. 强密码检验器（Strong Password Checker）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [420\. Strong Password Checker](https://leetcode-cn.com/problems/strong-password-checker/)

Difficulty: **困难**


一个强密码应满足以下所有条件：

1.  由至少6个，至多20个字符组成。
2.  至少包含一个小写字母，一个大写字母，和一个数字。
3.  同一字符**不能**连续出现三次 (比如 "...aaa..." 是不允许的, 但是 "...aa...a..." 是可以的)。

编写函数 strongPasswordChecker(s)，s 代表输入字符串，如果 s 已经符合强密码条件，则返回0；否则返回要将 s 修改为满足强密码条件的字符串所需要进行修改的**最小**步数。

插入、删除、替换任一字符都算作一次修改。


#### Solution

Language: **Java**

```java
​class Solution {
    public int strongPasswordChecker(String s) {
        int len=s.length();
        if(len<=3) return 6-len;
        boolean f1=false,f2=false,f3=false;
        List<Integer> rec=new ArrayList<>();
        int remain=s.length()-20;//还能删除的个数
        int re=remain;
        for(int i=0;i<len;i++){
            if('0'<=s.charAt(i)&&s.charAt(i)<='9') f1=true;
            if('a'<=s.charAt(i)&&s.charAt(i)<='z') f2=true;
            if('A'<=s.charAt(i)&&s.charAt(i)<='Z') f3=true;
            int cnt=1;
            while(i<s.length()-1&&s.charAt(i)==s.charAt(i+1)){
                cnt++;
                i++;
            }
            if(cnt>=3){
                if(remain>0){
                    if(cnt%3==0){
                        cnt--;
                        remain--;
                    }
                }
                if(cnt>=3)rec.add(cnt);
            }
        }
        int c=3;
        if(f1) c--;
        if(f2) c--;
        if(f3) c--;
        if(s.length()==4) return Math.max(2,c);
        if(s.length()==5) return Math.max(1,c);
        //检查重复,先删除，后替换
        for(int i=0;i<rec.size();i++){ //%3=1
            if(remain==1){
                remain=0;
                break;
            }
            if(remain>0&&rec.get(i)%3==1){
                int n=rec.get(i);
                rec.set(i,n-2);
                remain-=2;
            }
            
        }
        for(int i=0;i<rec.size();i++){ //%3=2
            if(remain==2||remain==1){
                remain=0;
                break;
            }
            if(remain>0){
                int n=rec.get(i);
                if(n>3){
                    int r=n-2;
                    rec.set(i,n-Math.min(remain,r));
                    remain=Math.max(remain-r,0);
                }
            }
        }
        int res=re-remain;
        if(remain>0) return res+c+remain;//删除余下的
        for(int a:rec){//替换
            res+=a/3;
            c-=a/3;
        }
        return res+(c>0?c:0);
    }
}
```
---
***参考：
[LeetCode](https://leetcode-cn.com/problems/strong-password-checker/)***
