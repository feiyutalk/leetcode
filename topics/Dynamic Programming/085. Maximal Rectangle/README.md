# 85. Maximal Rectangle

## #1 转化为直方图求解(AC)

个人认为这道题目的难度非常大，解法一是利用LeetCode84题的算法来求解的。首先遍历二维数组中的每一行，将其转化为直方图（直方图利用一个一维数组来存储），然后利用84题的算法求解直方图中最大矩形的面积。

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0) return 0;
        
        int m = matrix.length;
        int n = matrix[0].length;
        int[] heights = new int[n];
        for(int j=0; j<n; j++){
            if(matrix[0][j] == '1')
                heights[j] = 1;
        }
        int res = largestRectangleArea(heights);
        for(int i=1; i<m; i++){
            // 先改变heights数组的值 获得对应的直方图
            for(int j=0; j<n; j++){
                if(matrix[i][j] == '1')
                    heights[j] += 1;
                else
                    heights[j] = 0;
            }
            // 求解直方图中最大矩形的面积
            res = Math.max(res, largestRectangleArea(heights));
        }
        return res;
    }
    
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        int max = 0;
        for(int i=0; i<heights.length; i++){
            int minHeight = heights[i];
            if(i == heights.length-1 || heights[i] > heights[i+1])
                for(int j=i; j>=0; j--){ //底的宽度为 i-j+1
                    minHeight = Math.min(minHeight, heights[j]);
                    max = Math.max(max, minHeight*(i-j+1)); 
                }
        }
        return max;
    }
}
```

