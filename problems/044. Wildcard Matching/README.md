# 44. Wildcard Matching

这道题目和LeetCode第10题正则表达式匹配[Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)很类似，其解法也是非常类似的，都是通过动态规划的方式来求解，如果没有做过那道题目，建议先做一下。

这道题目我直接通过动态规划来求解，对于动态规划，我自己总结了三个步骤：

1. 定义状态
2. 获得初始状态值
3. 思考转移方程

对于如何定义状态，实际上是比较难定义的， 但是你通过分析题目要求解的结果是能够发现状态定义的方式的，因为题目要求的结果就是动态规划中最终的状态值。对于这道题目，我们定义dp\[i][j]表示长度为i的输入串和长度为j的模式串的匹配情况，我们要求解的最终状态值是dp\[s.length()][p.length()]。

对于如何获得初始状态值，只要分析边界条件就可以了，这里的边界条件有三种请客:

- 输入串和匹配串都是空串。dp\[0][0] = true
- 输入串为空，匹配串不为空。dp\[0][j] = dp\[0][j-1]，至于为什么是这个表达式，这里不提供严格的证明，只用一个例子来说明一下。假设我们的输入是: "", "a*"，这种情况dp\[0][2] = false，因为 dp\[0][1] = false, 而如果输入是: "", "**"，这种情况dp\[0][2] = true 因为， dp\[0][1] = true;
- 输入串非空，匹配串为空。这种情况比较简单，dp\[i][0] = false即可。

对于如何获得转移方程，这大概是动态规划题目的一个难点，一般需要根据题目做分类讨论，针对这道题目，我们做如何的分类讨论:

- `s.charAt(i-1) == p.charAt(j-1)` 此时，只要把这两个相同的字符消去，然后当前的匹配情况只取决于消去该字符后剩余的字符串的匹配情况。即 dp\[i][j] = dp\[i-1][j-1]
- `p.charAt(j-1) == '?'` 这种情况和上面的情况一样，也是消去一个字符。
- `p.charAt(j-1) == '*'`，这种情况比上面的稍微复杂一些，需要分析`*`可能指代什么
  - `*`指代空串，此时可以得到 `dp[i][j] = dp[i][j-1]`，这种情况相当于只消去了p字符串中的`*`号
  - `*`指代多个字符，此时可以得到`dp[i][j] = dp[i-1][j]`，相当于把输入串中的当前字符消掉。

最后的代码如下：

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null)
            return false;
        // 1. 定义状态
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        // 2. 获得初始状态值
        dp[0][0] = true;
        for(int j=1; j<=p.length(); j++){
            if(p.charAt(j-1) == '*')
                dp[0][j] = dp[0][j-1];
        }
        for(int i=1; i<=s.length(); i++){
            dp[i][0] = false;
        }
        // 3. 转移方程
        for(int i=1; i<=s.length(); i++){
            for(int j=1; j<=p.length(); j++){
                if(s.charAt(i-1) == p.charAt(j-1))
                    dp[i][j] = dp[i-1][j-1];
                else if(p.charAt(j-1) == '?')
                    dp[i][j] = dp[i-1][j-1];
                else if(p.charAt(j-1) == '*'){
                    dp[i][j] = (dp[i-1][j] || dp[i][j-1]);
                }else
                    dp[i][j] = false;
            }
        }
        return dp[s.length()][p.length()];
    }
}
```

