#583. Delete Operation for Two Strings

## #1 最大子序列[AC]

### 思路

该问题可以转化为求解两个字符串的最长子序列，如果我们找到了最长子序列，那么其他的字符就是我们要删掉的。

### 算法

```java
class Solution {
    /*
    两个字符串要完全相同，我们要找到两个字符串的最长公共子序列！
    我们可以通过动态规划的方法来求解！
    */
    public int minDistance(String word1, String word2) {
        if(word1 == null || word1.length() == 0)
            return word2 == null ? 0 : word2.length();
        if(word2 == null || word2.length() == 0)
            return word1 == null ? 0 : word1.length();
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m+1][n+1];
        for(int i=1; i<=m; i++){
            for(int j=1; j<=n; j++){
                int path1 = word1.charAt(i-1) == word2.charAt(j-1) ? dp[i-1][j-1] + 1 : 0;
                int path2 = dp[i-1][j];
                int path3 = dp[i][j-1];
                dp[i][j] = Math.max(path1, Math.max(path2, path3));
            }
        }
        return m + n - 2 * dp[m][n];
    }
}
```

### 复杂度分析

- 时间复杂度
- 空间复杂度