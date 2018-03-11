# 123. Best Time to Buy and Sell Stock III

## #1 动态规划[AC]

实际上我们可以把这道题目一般化为可进行`k`次交易，我们用状态表`dp[i][j]`表示进行了`i`次交易，并且已知第`j`天的价格时的最大收益。对于该状态的求解，我们遍历买入时间，从而求得在所有买入时间里，使得第`i`次交易在第`j`天卖出时收益最大的那个买入时间。所以，可以将状态转移方程描述如下:

```java 
for(int m=0; m<j; m++){
  profit = Math.max(profit, prices[j] - prices[m] + dp[i-1][m]);
}
```

完整代码如下:

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        int[][] dp = new int[3][prices.length];
        for(int i=0; i<dp.length; i++)
            dp[i][0] = 0;
        for(int j=0; j<dp[0].length; j++)
            dp[0][j] = 0;
        for(int i=1; i<dp.length; i++){
            for(int j=1; j<dp[0].length; j++){
                int profit = 0;
                for(int m=0; m<j; m++){
                    profit = Math.max(profit, prices[j] - prices[m] + dp[i-1][m]);
                }
                dp[i][j] = Math.max(dp[i][j-1], profit);
            }
        }
        return dp[2][prices.length-1];
    }
}
```

#### 复杂性分析:

- **时间复杂性：**$O(kn^2)$
- **空间复杂性：**$O(km)$

