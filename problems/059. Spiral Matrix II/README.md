# 59. Spiral Matrix II
## Description

```
Difficulty: Medium
```

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:

	[
	 [ 1, 2, 3 ],
	 [ 8, 9, 4 ],
	 [ 7, 6, 5 ]
	]
## Solution 1
  我们可以依次的填充，先填充最外圈，再填充次外圈等等，直到填充结束。

```java

class Solution {
    public int[][] generateMatrix(int n) {
        if(n == 0)
            return new int[0][0];
        
        int left = 0;
        int right = n-1;
        int top = 0;
        int down = n-1;
        int value = 1;
        int[][] result = new int[n][n];
        while(left<right){
            // top row
            for(int j=left; j<=right; j++){
                result[top][j] = value++;
            }
            top++;
            // right col
            for(int i=top; i<=down; i++){
                result[i][right] = value++;
            }
            right--;
            // down row
            for(int j=right; j>=left; j--){
                result[down][j] = value++;
            }
            down--;
            //left col
            for(int i=down;i>=top; i--){
                result[i][left] = value++;
            }
            left++;
        }
        if(n%2 == 1)
            result[left][left] = value++;
        return result;
    }
}

```

***

**enjoy life, coding now! :D**
