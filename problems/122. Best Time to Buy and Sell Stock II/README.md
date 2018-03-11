# 122. Best Time to Buy and Sell Stock II

## #1 动态规划[TLE]

我们定义状态`dp[i]`用来表示第`i`天的最大收益，我们知道对于第`i`天，也选择卖出，也可以选择不卖出(我们在研究第`i`天的时候，可以不考虑第`i`天进行买入的情况，因为这种情况不会带来最大收益)。如果在第`i`天进行卖出，我们需要找到`1..i-1`天里面价格最低的那一天进行买入，这样会使得卖出后收益最大；如果在第`i`天不进行卖出，那么`dp[i]=dp[i-1]`

通过以上分析，我们发现，对于`dp[i]`，它由两种可能的路径，一种是第`i`天卖出；另一种是第`i`天不卖出。我们只要取这两种路径中，收益最大的即可。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        int[] dp = new int[prices.length];
        dp[0] = 0;
        for(int i=1; i<prices.length; i++){
            int max = 0;
            for(int j=0; j<i; j++){
                if(dp[j] + prices[i] - prices[j] > max)
                    max = dp[j] + prices[i] - prices[j];
            }
            dp[i] = Math.max(dp[i-1], max);
        }
        return dp[prices.length-1];
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n^2)$
- **空间复杂性：**$O(n)$

## #2 贪心[AC]

从上面动态规划中，我们可以看出来，在判断`dp[i]`的最大收益的时候，对于在第`i`天卖出的情况，需要用$O(n)$的时间复杂度来进行计算，这导致整个算法的时间复杂度较高。那么，我们是否有更好的方法来避免这个计算呢？

我们首先定义`F(i)`表示第`i`天卖出的收益，`G(i)`表示第`i`天的最大收益：

<center>显然，$G(i) = max(G(i-1), F(i))$</center>

现在，我们主要分析一下$F(i)$的求解，我们先看一个例子，对于[1,2,3,5]这样的情况，显然5-1可以获得最大的收入，但是由于不限制交易次数，我们也可以这样交易(2-1) + (3-2) + (5-3)。这样的话，我们可以发现下面式子总是成立:

<center>$F(i) = max(G(j)+prices(i) - prices(j)) = max(G(j) + prices(i) - prices(i-1) + …+prices(j+1) - prices(j))$
</center>

好了，如果我们现在计算$F(j+1) =G(j) + prices(j+1) - prices(j)$，而$G(j+1) = max(G(j), F(j+1)) = max(G(j), G(j) + prices(j+1) - prices(j))$，从而我们发现，我们可以通过判断$prices[i]和prices[i-1]$的值来尽早进行剪枝。

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        int[] dp = new int[prices.length];
        dp[0] = 0;
        for(int i=1; i<prices.length; i++)
            if(prices[i] > prices[i-1])
                dp[i] = dp[i-1] + prices[i] - prices[i-1];
            else
                dp[i] = dp[i-1];
        return dp[prices.length-1];
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n)$
- **空间复杂性：**$O(n)$

