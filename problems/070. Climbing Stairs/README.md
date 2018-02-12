# 70. Climbing Stairs

## Solution 1 动态规划

这道题目可以通过动态规划来求解，我们定义状态`dp[i]`表示到第i个台阶共有几种方式，并初始化`dp[0] = 1`以及`dp[1]=1`，然后通过转移方程`dp[i] = dp[i-1] + dp[i-2]`来一步步的求解未知的解。

```java
class Solution {
    public int climbStairs(int n) {
        if(n <= 0)
            return 0;
        if(n == 1)
            return 1;
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2; i<=n; i++)
            dp[i] = dp[i-1] + dp[i-2];
        return dp[n];
    }
}
```

