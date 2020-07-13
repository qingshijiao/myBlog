---
title: 537. 复数乘法（Complex Number Multiplication）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [537\. 复数乘法](https://leetcode-cn.com/problems/complex-number-multiplication/)

Difficulty: **中等**


给定两个表示的字符串。

返回表示它们乘积的字符串。注意，根据定义 i<sup>2</sup> = -1 。

**示例 1:**

```
输入: "1+1i", "1+1i"
输出: "0+2i"
解释: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i ，你需要将它转换为 0+2i 的形式。
```

**示例 2:**

```
输入: "1+-1i", "1+-1i"
输出: "0+-2i"
解释: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i ，你需要将它转换为 0+-2i 的形式。 
```

**注意:**

1.  输入字符串不包含额外的空格。
2.  输入字符串将以 **a+bi** 的形式给出，其中整数 **a** 和 **b** 的范围均在 [-100, 100] 之间。**输出也应当符合这种形式**。


#### Solution

Language: **Java**

```java
class Solution {
    public String complexNumberMultiply(String a, String b) {
        int[] aa=trans(a);
        int[] bb=trans(b);
        int[] ans=new int[2];
        //System.out.println(aa[1]);
        ans[0]=aa[0]*bb[0]-aa[1]*bb[1];
        ans[1]=aa[1]*bb[0]+aa[0]*bb[1];
        StringBuilder sb=new StringBuilder();
        sb.append(ans[0]);
        sb.append('+');
        sb.append(ans[1]);
        sb.append('i');
        return sb.toString();
    }
    public int[] trans(String s){
        int len=s.length();
        char[] sChar=s.toCharArray();
        int count=0;
        int a=0;
        int b=0;
        int o1=0;
        int o2=0;
        int i=0;
        if(sChar[0]=='-'){
            i=1;
            o1=-1;
        }
        else o1=1;
        while(i<len&&Character.isDigit(sChar[i])){
            count=count*10+(sChar[i]-'0');
            i++;
        }
        a=o1*count;
        count=0;
        if(i<len&&sChar[i+1]=='-'){
            i+=2;
            o2=-1;
        }
        else {
           o2=1;
           i++; 
        }
        while(i<len&&Character.isDigit(sChar[i])){
            count=count*10+(sChar[i]-'0');
            i++;
        }
        b=o2*count;
        return new int[]{a,b};
    }
}
```

---java
public class Solution {

    public String complexNumberMultiply(String a, String b) {
        String x[] = a.split("\\+|i");
        String y[] = b.split("\\+|i");
        int a_real = Integer.parseInt(x[0]);
        int a_img = Integer.parseInt(x[1]);
        int b_real = Integer.parseInt(y[0]);
        int b_img = Integer.parseInt(y[1]);
        return (a_real * b_real - a_img * b_img) + "+" + (a_real * b_img + a_img * b_real) + "i";

    }
}
---


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/complex-number-multiplication/)***
