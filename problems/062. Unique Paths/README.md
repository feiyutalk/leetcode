# 062. Unique Paths

## Solution 1 动态规划

这道题目是经典的动态规划的题目，整个题目对于状态的定义以及转移方程的求解都是比较简单直观的。我们定义`dp[i][j]`为走到第`i-1`行和第`j-1`列交叉的格子的步数，并且得到初始状态值`dp[0][0] =1` `dp[i][0] = 1` `dp[0][j] = 1`，最后我们通过分析题目，发现除了第一行和第一列的格子，其他格子要走到该位置，只能通过从左边格子或者上边格子走过来，所以我们的转移方程为`dp[i][j] = dp[i-1][j] + dp[i][j-1]`。

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if(m <= 0 || n <= 0)
            return 0;
        int[][] dp = new int[m][n];
        for(int i=0; i<m; i++)
            dp[i][0] = 1;
        for(int j=0; j<n; j++)
            dp[0][j] = 1;
        for(int i=1; i<m; i++){
            for(int j=1; j<n; j++){
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```

