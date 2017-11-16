# 063. Unique Paths II

# Solution

这道题目和之前I是差不多的，就是多加了限制条件，整体上还是采用动态规划来求解，需要注意的就是在初始化的时候，如果遇到1，那么之后的值就都为默认值0。在做状态转化的时候，如果遇到1，那么不需要计算。

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if(obstacleGrid == null || obstacleGrid.length == 0)
            return 0;
        
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        for(int i=0; i<m; i++){
            if(obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for(int j=0; j<n; j++){
            if(obstacleGrid[0][j] == 1) break;
            dp[0][j] = 1;
        }
        
        for(int i=1; i<m; i++){
            for(int j=1; j<n; j++){
                if(obstacleGrid[i][j] == 1) continue;
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```

