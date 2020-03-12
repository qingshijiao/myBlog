---
title: 294.翻转游戏 II(flip game II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to determine if the starting player can guarantee a win.

For example, given s = "++++", return true. The starting player can guarantee a win by flipping the middle "++" to become "+--+".

Follow up:
Derive your algorithm's runtime complexity.


#### Solution

Language: **Java**

```java
public class Solution {
    public boolean canWin(String s) {
        for ( int i = 0; i < s.length() - 1; i ++ ){
            if ( s.charAt ( i ) == '+' && s.charAt( i + 1 ) == '+' ){
                StringBuilder sb = new StringBuilder ( s );
                sb.setCharAt ( i , '-');
                sb.setCharAt ( i + 1 ,'-');
                if ( !canWin ( sb.toString() ) )
                    return true;
            }
        }
        return false;
    }
}

```


#### Solution - backtracking

Language: **Java**

```java
public boolean canWin(String s) {
    if(s==null||s.length()==0){
        return false;
    }

   return canWinHelper(s.toCharArray());
}

public boolean canWinHelper(char[] arr){
    for(int i=0; i<arr.length-1;i++){
        if(arr[i]=='+'&&arr[i+1]=='+'){
            arr[i]='-';
            arr[i+1]='-';

            boolean win = canWinHelper(arr);

            arr[i]='+';
            arr[i+1]='+';

            //if there is a flip which makes the other player lose, the first play wins
            if(!win){
                return true;
            }
        }
    }

    return false;
}
```

#### Solution - dp

Language: **Java**

```java
public class Solution {
    public boolean canWin(String s) {
        char[] arr = s.toCharArray();
        for(int i = 1; i < s.length(); i++) {
            if(arr[i] == '+' && arr[i - 1] == '+') {
                arr[i] = '-';
                arr[i - 1] = '-';
                String next = String.valueOf(arr);
                if(!canWin(next)) {
                    return true;
                }
                arr[i] = '+';
                arr[i - 1] = '+';
            }
        }

        return false;
    }
}　
```


---
***参考：
[lightwindy](https://www.cnblogs.com/lightwindy/p/9666939.html)***
