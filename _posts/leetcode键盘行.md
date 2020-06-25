---
title: 500. 键盘行 (Keyboard Row)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [500\. Keyboard Row](https://leetcode-cn.com/problems/keyboard-row/)

Difficulty: **简单**


给定一个单词列表，只返回可以使用在键盘同一行的字母打印出来的单词。键盘如下图所示。

![American keyboard](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/keyboard.png)

**示例：**

```
输入: ["Hello", "Alaska", "Dad", "Peace"]
输出: ["Alaska", "Dad"]
```

**注意：**

1.  你可以重复使用键盘上同一字符。
2.  你可以假设输入的字符串将只包含字母。


#### Solution

Language: **Java**

```java
​class Solution {
    public String[] findWords(String[] words) {
        String[] a=new String[]{"QWERTYUIOPqwertyuiop","ASDFGHJKLasdfghjkl","ZXCVBNMzxcvbnm"};
        List<String> res=new ArrayList<>();
        for(int i=0;i<words.length;i++)
        {
            int flag=-1;
            if(a[0].indexOf(words[i].charAt(0))>=0)
            {
                flag=0;
            }else if(a[1].indexOf(words[i].charAt(0))>=0)
            {
                flag=1;
            }else if(a[2].indexOf(words[i].charAt(0))>=0)
            {
                flag=2;
            }
            for(int j=0;j<words[i].length();j++)
            {
                if(a[flag].indexOf(words[i].charAt(j))<0)
                {
                    flag=-1;
                    break;
                }
            }
            if(flag!=-1)
            res.add(words[i]);
        }
        String[] ans=new String[res.size()];
        for(int i=0;i<ans.length;i++)
        {
            ans[i]=res.get(i);
        }
        return ans;
    }
}
```


---
***参考：
[leetcode](https://leetcode-cn.com/problems/keyboard-row/)***
