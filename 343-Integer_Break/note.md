# 343. Integer Break
## Description

```
Difficulty: Easy
```

Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

Note: You may assume that n is not less than 2 and not larger than 58.

## Solution 1
3 = 1+1+1  3 = 2+1  res= 1*1*1 = 1   res2 = 2 *1 =2  return 2;

怎么考虑？

有一个想法  我们怎么看待这个整数？

整数n  n = i+j;

dp[n]

dp[3] = 2

dp[n] = dp[i+j] 有什么好处？

n=i+j  res1 = i*j dp[i] dp[j]

做一个比较   i dp[i]   j dp[j]

n = 6 

n = 1 + 5

n = 2 + 4 res1 = 2 * 4 dp[2]: 2= 1+1 dp[2]=1  dp[4]

n = 3 + 3 

n = 4 + 2

n = 5 + 1

n = 4 

n = 1 + 3 dp[1]=0 dp[3]=1

n = 2 + 2

n = 3 + 1

n = 3 

n = 1 + 1 + 1 dp[3] = 1;

我们接触了动态规划的解题模式，我们知道用已知来推未知的一个解题观点。所以，我们虽然求解的是第n步的答案，但是我们需要依赖前面所有的答案。所以，我们需要记录前面所有的答案。我们通过整数看成两个数之和，这是一种技巧。

```java

public class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n+1];
        for(int i=1;i<n;i++){
            for(int j=1; j<n+1; j++){
               if(i+j<=n){
                   dp[i+j]=Math.max(Math.max(i,dp[i])*Math.max(j,dp[j]),dp[i+j]);
               } 
            }
        }
        return dp[n];
    }
}

```

***

**enjoy life, coding now! :D**
