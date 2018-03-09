# 64. Minimum Path Sum

## #1 动态规划(AC)

这道题目的场景和[Unique Paths](https://leetcode.com/problems/unique-paths)、[Unique Paths II](https://leetcode.com/problems/unique-paths-ii)是差不多的，区别在于后者问的是不同的可行路线，而前者问的是最小的路径和，都可以采用动态规划的思路来求解。

- 定义状态: `dp[i][j]`表示走到第`i`行第`j`列的最小路径和。
- 初始化状态第一行的值以及第一列的值可直接求得，因为这两条路径都是只有唯一的走法。
- 状态转移方程：对于`dp[i][j]`即走到第`i`行第`j`列，此时只能两种转移路径，一种是从第`i-1`行第`j`列走过来，另一种是从第`i`行第`j-1`列走过来。故转移方程为`dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j];`

#### 复杂性分析：

- **时间复杂性：**$O(n^2)$
- **空间复杂性：**$O(n^2)$

```java
class Solution {
    public int minPathSum(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];
        dp[0][0] = grid[0][0];
        for(int j=1; j<n; j++)
            dp[0][j] = dp[0][j-1] + grid[0][j];
        for(int i=1; i<m; i++)
            dp[i][0] = dp[i-1][0] + grid[i][0];
        for(int i=1; i<m; i++)
            for(int j=1; j<n; j++){
                dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
            }
        return dp[m-1][n-1];
    }
}
```

