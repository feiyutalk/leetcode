# 072. Edit Distance

## #1 动态规划(AC)

编辑距离在自然语言处理中是非常有用的一个概念，当时我在算法交流会上也讲过这个话题，大家可以先去看一下当时我的笔记以及ppt:[最小编辑距离](https://github.com/conghuaicai/happy-algorithms/blob/master/%E7%AC%AC01%E6%9C%9F/%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%9C%80%E5%B0%8F%E7%BC%96%E8%BE%91%E8%B7%9D%E7%A6%BB%E7%AE%97%E6%B3%95.md) 

这个笔记以及ppt对最小编辑距离的介绍以及用动态规划方法来求解最小编辑距离还是讲得比较清楚的。下面就不再赘述，直接放上代码:

```java
class Solution {
    public int minDistance(String word1, String word2) {
        if(word1.equals(word2)) return 0;
        if(word1.length() == 0) return word2.length();
        if(word2.length() == 0) return word1.length();
        // 1. define status dp[i][j] the minimal edit distance between word1(1..i) and word2(1..j)
        int[][] dp = new int[word1.length() + 1][word2.length() + 2];
        // 2. initialization
        for(int i=0; i<=word1.length(); i++){
            dp[i][0] = i; //word1 is not empty, while word2 is empty -> delete
        }
        for(int j=0; j<=word2.length(); j++){
            dp[0][j] = j; //word2 is not empty, while word1 is empty -> add
        }
        // 3. transform
        for(int i=1; i<=word1.length(); i++){
            for(int j=1; j<=word2.length(); j++){
                int insert = dp[i][j-1] + 1;
                int delete = dp[i-1][j] + 1;
                int replace = dp[i-1][j-1] + (word1.charAt(i-1) == word2.charAt(j-1)? 0 : 1);
                dp[i][j] = Math.min(Math.min(insert, delete), replace);
            }
        }
        return dp[word1.length()][word2.length()];
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(nm)$
- **空间复杂性：**$O(nm)$