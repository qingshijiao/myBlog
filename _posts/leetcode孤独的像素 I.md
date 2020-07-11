---
title: 531.孤独的像素 I（Lonely Pixel I）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a picture consisting of black and white pixels, find the number of black lonely pixels.

The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

A black lonely pixel is character 'B' that located at a specific position where the same row and same column don't have any other black pixels.

Example:

Input: 
[['W', 'W', 'B'],
 ['W', 'B', 'W'],
 ['B', 'W', 'W']]

Output: 3
Explanation: All the three 'B's are black lonely pixels. 
Note:

The range of width and height of the input 2D array is [1,500].


#### Solution

Language: **Java**

```java
public int findLonelyPixel(char[][] picture) {
    int n = picture.length, m = picture[0].length;
     
    int[] rowCount = new int[n], colCount = new int[m];
    for (int i=0;i<n;i++)
        for (int j=0;j<m;j++)
            if (picture[i][j] == 'B') { rowCount[i]++; colCount[j]++; }
 
    int count = 0;
    for (int i=0;i<n;i++)
        for (int j=0;j<m;j++)
            if (picture[i][j] == 'B' && rowCount[i] == 1 && colCount[j] == 1) count++;
                 
    return count;
}
```

---
***参考：
[lightwindy](https://www.cnblogs.com/lightwindy/p/9666798.html)***
