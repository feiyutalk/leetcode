# 139. Word Break

## #1 动态规划[AC]

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if(s == null || s.length() == 0) return false;
        HashSet<String> set = new HashSet<>(wordDict);
        int n = s.length();
        boolean[] dp = new boolean[n+1];
        dp[0] = true;
        for(int i=1; i<=n; i++){
            for(int j=i; j>0; j--){
                String sub = s.substring(i-j, i);
                if(set.contains(sub)){
                    if(dp[i-j] == true){
                        dp[i] = true;
                        break;
                    }
                }
            }
        }
        return dp[n];
    }
}
```

