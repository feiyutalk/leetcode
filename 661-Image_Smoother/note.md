# 661. Image Smoother
## Description

```
Difficulty: Easy
```

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.

**Example 1:**

```

Input:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
Output:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
Explanation:
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0

```
## Solution 1
  去对数组做一个二重循环，对于这种二维数组元素的周围元素的一个遍历，我们有固定的模板。

```java

int m = ..// total row number
int n = .. // total column number
int row = ..
int col = ..
for(int i=-1; i<2; i++){
  for(int j=-1;j<2; j++){
	 int r = row + i;
     int c = col + j;	
     if(r<0 || r>=m || c<0 || c>=n)
		continue;
     //add operation
  }
}

```

```java

class Solution {
    public int[][] imageSmoother(int[][] M) {
        if(M == null || M.length == 0)
            return M;
        int m = M.length;
        int n = M[0].length;
        int[][] result  = new int[m][n];
        for(int row = 0; row < m; row++){
            for(int col = 0; col < n; col++){
                int sum = 0;
                int count = 0;
                for(int i=-1; i<2; i++){
                    for(int j=-1; j<2; j++){
                        int r = row + i;
                        int c = col + j;
                        if(r<0 || r>=m || c<0 || c>=n)
                            continue;
                        sum += M[r][c];
                        count++;
                    }
                }
                result[row][col] = (sum/count);
            }
        }
        return result;
    }
}
```

***

**enjoy life, coding now! :D**
