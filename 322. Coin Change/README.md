# 322. Coin Change
## Description

```
Difficulty: Medium
```

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

coins = [1, 2, 5], amount = 11

return 3 (11 = 5 + 5 + 1)

Example 2:

coins = [2], amount = 3

return -1.
## Solution 1 动态规划
  动态规划的典型模式。在求解动态规划的时候，我们一般需要一个全局的结果数组。根据不同的题目背景，我们需要修改不不同的判断因子，但是整体的动态规划的模式是不会有变化的。

  我们做动态规划的时候，通过就是利用未知来推已知，这就意味着将未知的问题转化为已知问题，但是！！！！未知转化成已知的时候，往往有多个转化的路径！我们再做当前未知问题的时候，需要考虑的不仅仅只是转化，我们还需要注意在多个路径之间做比较！

```java

public class Solution {
    public int coinChange(int[] coins, int amount) {
        //我们发现当前的amount可以看成是之前的已知的amount的和！
        //先考虑异常
        if(coins == null || coins.length == 0 || amount <= 0)
            return 0;
        //动态规划  result : 1 ~ amount; 一个结果
        /*
        i = 11   11 = 1 + 10 ， 2 + 9 ， 3 + 8 ...
        
        */
        int[] minNumber = new int[amount+1];
        for(int i=1; i<= amount; i++){
            minNumber[i] = Integer.MAX_VALUE;
            for(int j=0; j<coins.length; j++){
                if(coins[j]<=i && minNumber[i - coins[j]] != Integer.MAX_VALUE){
                    minNumber[i] = Math.min(minNumber[i], 1 + minNumber[i - coins[j]]);
                }
            }
        }
        if(minNumber[amount] == Integer.MAX_VALUE)
            return -1;
        return minNumber[amount];
    }
}
```

***

**enjoy life, coding now! :D**
