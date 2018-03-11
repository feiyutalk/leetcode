# 115. Distinct Subsequences

## #1 动态规划[AC]

```java
class Solution {
    public int numDistinct(String s, String t) {
        if(s == null || t == null)
            return 0;
        int[][] dp = new int[s.length()+1][t.length()+1];
        dp[0][0] = 1;
        for(int i=1; i<dp.length; i++)
            dp[i][0] = 1;
        for(int i=1; i<dp.length; i++)
            for(int j=1; j<dp[0].length; j++)
                if(s.charAt(i-1) == t.charAt(j-1))
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                else
                    dp[i][j] = dp[i-1][j];
        return dp[s.length()][t.length()];
    }
}
```

