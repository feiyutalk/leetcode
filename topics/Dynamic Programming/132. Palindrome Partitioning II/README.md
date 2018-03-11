# 132. Palindrome Partitioning II

## #1 动态规划[AC]

这道题目在求解所有回文子串的基础进行扩展，使得发现回文子串的基础上，对原始字符串进行切割，让切割后的每个子串都是回文串。我们需要一个`boolean[][] isPal`用来记录每个从`i`到`j`的子串是否为回文串。并且我们定义动态规划的状态`cuts[i]`表示长度为`i`的字符串进行切割，使得各个子串都是回文串的最小切割次数。紧接着， 我们来分析状态转移过程，对于`cuts[i]`我们可以遍历所有`i`之前的位置可能位置`j`，先判断`S[j->i]`是否为回文，如果是的话，那么`j`就是一个可能的切割位置。

```java
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() == 0)
            return 0;
        int n = s.length();
        boolean[][] isPal = new boolean[n][n];//起始位置为i，终止位置为j的子串是否为回文
        int[] cuts = new int[n];
        for(int i=0; i<n; i++){
            int min = i;
            for(int j=0; j<=i; j++){
                if(s.charAt(i) == s.charAt(j) && (i-j<3 || isPal[j+1][i-1])){
                    isPal[j][i] = true;
                    min = (j==0?0:Math.min(min, cuts[j-1]+1));
                }
            }
            cuts[i] = min;
        }
        return cuts[n-1];
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n^2)$

- **空间复杂性：**$O(n^2)$

  ​