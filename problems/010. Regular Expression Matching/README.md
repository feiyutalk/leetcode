# 10. Regular Expression Matching

## #1 动态规划[AC]

在正则表达式中，由于不同的字符会有不同的匹配规则，其中`.`和`*`比较特别，需要对这两类字符进行分类讨论。

- 定义状态`dp[i][j]`表示输入串长度为i，模式串长度为j时，是否能匹配。
- 初始化状态值：
  - 输入串为空，模式串为空： `dp[0][0]`必然可以匹配，即`dp[0][0]=true`
  - 输入串非空，模式串为空：由于模式串为空，此时必然不可匹配，即`dp[i][0]=false,i>0`
  - 输入串为空，模式串非空：此时如果模式串中有`*`，则是可以匹配0个前面的字符的，所有我们通过条件`p.charAt(j-1) == '*' && dp[0][j-2]`来判断是否可匹配
- 转移方程，转移方程表示通过已知的状态值来求解未知的状态值，在这里就是我们要求解`dp[i][j]`，但是对于所有长度小于`i`的输入串和长度小于`j`的模式串，我们已知其匹配情况。现在，我们怎么利用前面的信息，来得到`dp[i][j]`的值。我们首先需要分析模式串的当前字符来做判断:
  - `p.charAt(j-1) == s.charAt(i-1)`当前模式串字符一样，可以将当前字符匹配掉，然后状态转化如下:`dp[i][j] = dp[i-1][j-1];`
  - `p.charAt(j-1) == '.'`当前模式串字符为`.`，可以匹配任意的字符，可以将当前输入串字符匹配掉，然后状态转化为:`dp[i][j] = dp[i-1][j-1]`
  - `p.charAt(j-1) == '*'`由于`*`可以匹配0个或多个它的上一个字符，所以根据上一个字符的不同还需要做不同的分析：
    - `p.charAt(j-2) != s.charAt(i-1) && p.charAt(j-2) != '.'`，这种情况说明上一个字符即不是`.`，也不和输入串的当前字符一样，所有无法用一个或多个上一个字符对输入串进行匹配，此时`*`只能匹配0个上一个字符:`dp[i][j] = dp[i][j-2];`
    - 如果是这个条件里，说明上一个字符和输入串的当前字符是可以进行匹配的，故此时`*`即可以匹配0个前一个字符，也可以匹配1个前一个字符，也可以匹配多个前一个字符:`dp[i][j] = (dp[i][j-1] || dp[i-1][j] || dp[i][j-2])`

整个题目的难点在于发现该题目能够用动态规划的方式进行求解，并且在求解转移方程的时候，根据模式串当前字符的不同，进行不同的分类讨论。

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null) return false;
        
        //定义状态
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        //初始状态赋值
        dp[0][0] = true;
        for(int i=1; i<=s.length(); i++)
            dp[i][0] = false;
        for(int j=1; j<=p.length(); j++)
            if(p.charAt(j-1) == '*' && dp[0][j-2])
                dp[0][j] = true;
        
        //利用初始状态值 以及 转移方程 求解未知状态值， 直到最终状态
        for(int i=1; i<=s.length(); i++){
            for(int j=1; j<=p.length(); j++){
                //case 1
                if(p.charAt(j-1) == s.charAt(i-1))
                    dp[i][j] = dp[i-1][j-1];
                else if(p.charAt(j-1) == '.')
                    dp[i][j] = dp[i-1][j-1];
                else if(p.charAt(j-1) == '*'){
                    if(p.charAt(j-2) != s.charAt(i-1) && p.charAt(j-2) != '.')
                        dp[i][j] = dp[i][j-2];
                    else
                        dp[i][j] = (dp[i][j-1] || dp[i-1][j] || dp[i][j-2]);
                }else
                    dp[i][j] = false;
            }
        }
        return dp[s.length()][p.length()];
    }
}
```

