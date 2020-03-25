---
title: 319.灯泡开关 (Bulb Switcher)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [319\. 灯泡开关](https://leetcode-cn.com/problems/bulb-switcher/)

Difficulty: **中等**


初始时有 _n _个灯泡关闭。 第 1 轮，你打开所有的灯泡。 第 2 轮，每两个灯泡你关闭一次。 第 3 轮，每三个灯泡切换一次开关（如果关闭则开启，如果开启则关闭）。第 _i_ 轮，每 _i _个灯泡切换一次开关。 对于第 _n _轮，你只切换最后一个灯泡的开关。 找出 _n _轮后有多少个亮着的灯泡。

**示例:**

```
输入: 3
输出: 1
解释:
初始时, 灯泡状态 [关闭, 关闭, 关闭].
第一轮后, 灯泡状态 [开启, 开启, 开启].
第二轮后, 灯泡状态 [开启, 关闭, 开启].
第三轮后, 灯泡状态 [开启, 关闭, 关闭].

你应该返回 1，因为只有一个灯泡还亮着。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int bulbSwitch(int n) {

       return (int)Math.sqrt(n);

        /*
        约数为奇数的最后才会亮着， 同时约数是成对存在的，什么时候会奇数？
        1 4 9 完全平方数， 两个约数相等的情况，转化为求1~n中完全平方数的个数。
        */
        // int i=0;
        // for(i=1; i*i <= n; i++){

        // }
        // return i-1;

        /*
        求1 ~ n中约数为奇数的个数， 超时
        */
        // if(n < 0) return Integer.MIN_VALUE;
        // if(n == 0) return 0;
        // int count = 0;
        // for(int i=1 ; i<= n; i++){
        //     int num_yueshu = numOfYueShue(i);
        //     count += (num_yueshu % 2);
        // }
        // return count;

        /*
        方法一， 模拟过程 超时
        */
        // if(n <=0 ) return 0;
        // if(n == 1) return 1;
        // int[] light =  new int[n];
        // Arrays.fill(light, 1);
        // for(int round =2; round<= n; round++){

        //     for(int i = round-1; i<n ;i += round){
        //         light[i] = -light[i];
        //     }
        // }
        // int count = 0;
        // for(int x: light){
        //     if(x == 1) count++;
        // }
        // return count;
    }
    private int numOfYueShue(int n){
        if(n <= 0) return 0;
        int count = 0;
        int i=0;
        for(i =1 ; i*i < n ;i++){
            if(n % i == 0){
                count += 2;
            }
        }
        if(i*i == n) count++;
        return count;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/bulb-switcher/submissions/)***
