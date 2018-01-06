# 634. Find the Derangement of An Array

```java
class Solution {
    public int findDerangement(int n) {
        if(n <= 1) return 0;
        long[] dp = new long[n + 1];
        long mod = 1000000007;
        dp[2] = 1;
        for(int i = 3; i < dp.length; i++){
            dp[i] = (long)(i - 1) * (dp[i - 1] + dp[i - 2]) % mod;
        }
        return (int)dp[dp.length - 1];
    }
}
```

