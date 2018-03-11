# 91. Decode Ways

## #1 动态规划(AC)

- 状态`dp[i]`表示解码前`i`的数字时，可能的解码方式。
- 初始状态值`dp[0] = 1`(该值的设置没有实际意义，只是为了保证状态转移方程的一致性)，`dp[1]=1`。
- 转移方程，由于0的存在，需要针对0分类讨论:
  - 当前字符为0，此时考虑0和上一个字符是否可以被解码，如果不行，直接返回0；否则`dp[i] = dp[i-2]`，此时0和上一个字符被解码为一个字母；
  - 当前字符不为0，同样考虑当前字符是否可以和上一个字符一起被解码为一个字符，如果可以有: `dp[i] = dp[i-2] + dp[i-1]`；否则 `dp[i] = dp[i-1]`

```java
class Solution {
    public int numDecodings(String s) {
        if(s == null || s.length() == 0) return 0;
        if(s.charAt(0) == '0') return 0;
        int n = s.length();
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2; i<=n; i++){
            if(s.charAt(i-1) == '0'){
                if(s.charAt(i-2) < '1' || s.charAt(i-2) > '2') return 0;
                else
                    dp[i] = dp[i-2];
            }else{
                if(s.charAt(i-2) != '0' && Integer.valueOf(s.substring(i-2, i)) <= 26)
                    dp[i] = dp[i-2] + dp[i-1];
                else
                    dp[i] = dp[i-1];
            }
        }
        return dp[n];
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n)$
- **空间复杂性：**$O(1)$

