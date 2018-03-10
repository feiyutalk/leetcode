# 322. Coin Change

## #1 递归[TLE]

该问题可以形式化的表示为: $min_x \sum_{i=0}^{n-1}x_i, subject to \sum_{i=0}^{n-1}x_{i}*c_{i}=S$，我们可以暴力求解该问题，枚举出满足上述条件的所有$[x_0…x_{n-1}]$集合，并计算每个集合的硬币数量，然后返回最小的那个。

```java
public class Solution {    

    public int coinChange(int[] coins, int amount) {
        return coinChange(0, coins, amount);
    }

    private int coinChange(int idxCoin, int[] coins, int amount) {
        if (amount == 0)
            return 0;
        if (idxCoin < coins.length && amount > 0) {
            int maxVal = amount/coins[idxCoin];
            int minCost = Integer.MAX_VALUE;
            for (int x = 0; x <= maxVal; x++) {
                if (amount >= x * coins[idxCoin]) {
                    int res = coinChange(idxCoin + 1, coins, amount - x * coins[idxCoin]);
                    if (res != -1)
                        minCost = Math.min(minCost, res + x);
                }                    
            }           
            return (minCost == Integer.MAX_VALUE)? -1: minCost;
        }        
        return -1;
    }  
}
```

## #2 递归+缓存[AC]

首先我们作如下定义:

>F(S) - 使用$[c_0…c_{n-1}]$对数值S进行找零所需要的最小硬币数量

我们可以发现，经过这样的定义之后，该问题有最优子结构，这是解决动态规划问题的关键。换句话说，原问题的最优解可以由其子问题的最优解构造出来。但是，我们怎么将原问题拆解成子问题？我们作如下拆解:$F(S)=F(S-C)+1$，但是我们并不知道最后一个硬币的数值为多少，我们需要去枚举所有的可能，然后选择最小的。

![](https://leetcode.com/media/original_images/322_coin_change_tree.png)

```java
public class Solution {

    public int coinChange(int[] coins, int amount) {        
        if (amount < 1) return 0;
        return coinChange(coins, amount, new int[amount]);
    }

    private int coinChange(int[] coins, int rem, int[] count) {
        if (rem < 0) return -1;
        if (rem == 0) return 0;
        if (count[rem - 1] != 0) return count[rem - 1];
        int min = Integer.MAX_VALUE;
        for (int coin : coins) {
            int res = coinChange(coins, rem - coin, count);
            if (res >= 0 && res < min)
                min = 1 + res;
        }
        count[rem - 1] = (min == Integer.MAX_VALUE) ? -1 : min;
        return count[rem - 1];
    }
}
```

## #3 动态规划[AC]
 ![](https://leetcode.com/media/original_images/322_coin_change_table.png)

```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        int max = amount + 1;             
        int[] dp = new int[amount + 1];  
        Arrays.fill(dp, max);  
        dp[0] = 0;   
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.length; j++) {
                if (coins[j] <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```


