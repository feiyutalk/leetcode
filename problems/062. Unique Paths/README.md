# 062. Unique Paths

# Solution

这道题目是典型的动态规划的题目，当前位置只能从左边或者上边到达，所以当前总步数是等于左边的总步数➕上边的总步数，用动态规划依次打表就可以了。

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

