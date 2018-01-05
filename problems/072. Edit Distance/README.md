# 072. Edit Distance

```java
class Solution {
    public int minDistance(String word1, String word2) {
        String s = word1;
        String t = word2;
        if(s.equals(t)) return 0;
        if(s.length() == 0)
            return t.length();
        if(t.length() == 0)
            return s.length();
        // define status dp[i][j] the minimal dist between si and tj
        int dp[][] = new int[s.length()+1][t.length()+1];
        //init
        for(int i=0; i<dp.length; i++){
            dp[i][0] = i;
        }
        for(int j=0; j<dp[0].length; j++){
            dp[0][j] = j;
        }
        //transform
        for(int i=1; i<dp.length; i++){
            for(int j=1; j<dp[0].length; j++){
                int path1 = dp[i-1][j] + 1;
                int path2 = dp[i][j-1] + 1;
                int path3 = dp[i-1][j-1] + (s.charAt(i-1) == t.charAt(j-1) ? 0 : 1);
                dp[i][j] = Math.min(Math.min(path1, path2), path3);
            }
        }
        return dp[dp.length-1][dp[0].length-1];
    }
}
```

