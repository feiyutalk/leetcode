# 552. Student Attendance Record II
## Description

```
Difficulty: Hard
```
Given a positive integer n, return the number of all possible attendance records with length n, which will be regarded as rewardable. The answer may be very large, return it after mod 109 + 7.

A student attendance record is a string that only contains the following three characters:

1. 'A' : Absent.
1. 'L' : Late.
1. 'P' : Present.

A record is regarded as rewardable if it doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

**Example 1:**

```

Input: n = 2
Output: 8 
Explanation:
There are 8 records with length 2 will be regarded as rewardable:
"PP" , "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" won't be regarded as rewardable owing to more than one absent times. 

```

## Solution 1

利用 dp[n][A][L] 表示什么？ 
 
n: n次课 长度为n
 
A: 包含的A字符的个数
 
L: 连续的以L结尾的字符串的个数
 
我们就可以利用已知推未知！！！

dp[1] = {{1,1,0},{1,0,0}}; 
 
dp[2][0][0] = dp[1][0][0] + dp[1][0][1] + dp[1][0][2] 
 
dp[2][0][1] = dp[1][0][0]
 
dp[2][0][2] = dp[1][0][1]
 
dp[2][1][0] = sum(dp[1][0]) + sum(dp[1][1])
 
dp[2][1][1] = dp[1][1][0]
 
dp[2][1][2] = dp[1][1][1]
 
一般化

dp[n][0][0] = sum(dp[n-1][0])
 
dp[n][0][1] = dp[n-1][0][0]
 
dp[n][0][2] = dp[n-1][0][1]
 
dp[n][1][0] = sum(dp[n-1][0]) + sum(dp[n-1][1])
 
dp[n][1][1] = dp[n-1][1][0]
 
dp[n][1][2] = dp[n-1][1][1]

动态规划就是通过已知去推未知的一个过程，那么当前的未知又会变成下一个未知的已知。我们可以通过特殊结论的分析，然后将结论一般化，这样的过程来简化我们的分析

```java

public class Solution {
    private final int MOD = 1000000007;
    public int checkRecord(int n) {
    /*
   
    */
     int[][] dp = {{1,1,0},{1,0,0}};
     for(int i=2; i<=n; i++){
         int [][] dpi = {{0,0,0},{0,0,0}};
         dpi[0][0] = (int)sum(dp[0]);
         dpi[0][1] = dp[0][0];
         dpi[0][2] = dp[0][1];
         dpi[1][0] = (int)((sum(dp[0])+sum(dp[1])) % MOD);
         dpi[1][1] = dp[1][0];
         dpi[1][2] = dp[1][1];
         dp = dpi;
     }
        return  (int)((sum(dp[0])+sum(dp[1])) % MOD);
    }
    
    public long sum(int[] nums){
        long ans = 0;
        for(int n : nums){
            ans += n;
        }
        return ans % MOD;
    }
}
```

***

**enjoy life, coding now! :D**
