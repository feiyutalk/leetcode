# 474. Ones and Zeros

# Solution

这道题目一开始的想法是先对字符串按照长度排序，然后先把长度小的匹配掉，然后匹配长度大的，后来发现这种想法是错的。后面看了解答，说这道题目是典型的0-1背包问题，最后是用动态规划来解决的，前面也做了不少动态规划的题目了， 也总结了动态规划需要解决的三个问题，最后动态规划问题都会被形象的描述为打表，之前的表格都是二维的，这次参考的答案，用动态规划打表后是三维的。

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int length =  strs.length;
        int[][][] dp = new int[length+1][m+1][n+1];
        for(int i=0; i<length+1; i++){
            int[] nums = new int[]{0,0};
            if(i>0){
                nums = calculate(strs[i-1]);
            }
            for(int j=0; j<m+1; j++){
                for(int k=0; k<n+1; k++){
                    if(i == 0){
                        dp[i][j][k] = 0;
                    }else if(j>=nums[0] && k>=nums[1]){
                        dp[i][j][k] = Math.max(dp[i-1][j][k], 1+dp[i-1][j-nums[0]][k-nums[1]]);
                    }else{
                        dp[i][j][k] = dp[i-1][j][k];
                    }
                }
            }
        }
        return dp[length][m][n];
    }
    
    private int[] calculate(String str){
        int[] res = new int[]{0,0};
        for(char c : str.toCharArray()){
            if(c == '0') res[0]++;
            else res[1]++;
        }        
        return res;
    }
}
```

