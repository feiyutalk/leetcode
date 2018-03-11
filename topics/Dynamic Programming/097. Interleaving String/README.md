# 097. Interleaving String

使用动态规划来求解。

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if(s1.length() + s2.length() != s3.length())
            return false;
        boolean[][] dp = new boolean[s1.length()+1][s2.length()+1];
        dp[0][0] = true;
        for(int i = 0; i<s1.length(); i++)
            if(s1.charAt(i) == s3.charAt(i))
                dp[i+1][0] = dp[i][0];
            else
                dp[i+1][0] = false;
       for(int j=0; j<s2.length(); j++)
           if(s2.charAt(j) == s3.charAt(j))
               dp[0][j+1] = dp[0][j];
           else
               dp[0][j+1] = false;
        
       for(int i=1; i<dp.length; i++){
           for(int j=1; j<dp[0].length; j++){
               dp[i][j] = (dp[i-1][j] && (s1.charAt(i-1) == s3.charAt(i+j-1)) || 
                          (dp[i][j-1] && (s2.charAt(j-1) == s3.charAt(i+j-1))));
           }
       }
       
       return dp[s1.length()][s2.length()];
    }
}
```

