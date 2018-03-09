# 32. Longest Valid Parentheses

## #1 暴力求解[TLE]

对于输入串，我们可以取暴力搜索其所有的子串，然后对每个子串判断其是否为有效的括号对，最后保存最大的有效子串的长度。

```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push('(');
            } else if (!stack.empty() && stack.peek() == '(') {
                stack.pop();
            } else {
                return false;
            }
        }
        return stack.empty();
    }
    public int longestValidParentheses(String s) {
        int maxlen = 0;
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 2; j <= s.length(); j+=2) {
                if (isValid(s.substring(i, j))) {
                    maxlen = Math.max(maxlen, j - i);
                }
            }
        }
        return maxlen;
    }
}
```

#### 复杂度分析:

- **时间复杂度**： $O(n^3)$，总共有$O(n^2)$的时间用于搜索所有的子串，对于每个子串，需要花费$O(n)$的时间检查是否为有效串。
- **空间复杂度**：$O(n)$，需要一个栈深为n的存储空间。

## #2 动态规划[AC]

- 状态定义：
  - 我们定义动态规划的状态dp[i]表示为以s[i]结尾的子串的最大有效括号对
- 初始状态
  - `dp[0]`表示以第一个字符结尾的子串，由于有效的括号对长度至少要为2，所以有`dp[0]=0`
- 转移方程
  - 如果当前遇到的字符为'('，那么此时以该字符结尾的子串不可能是有效的括号对，故此时`dp[i]=0`
  - 如果当前遇到的字符为')'，那么我们需要判断上一次字符的情况:
    - 如果上一个字符是'('，那么`dp[i]=2`
    - 如果上一个字符是')'，那此时有可能出现`(())`这样的场景，我们需要定位到以`s[i-1]`结尾的最长有效括号对的上一个位置，如果是`(`，则`dp[i]=dp[i-1]+dp[i-dp[i-1]-2]+2`，这里说明一下，其中`dp[i-1]`是上一个字符的最长有效对，`dp[i-dp[i-1]-2]`是指去掉上一个字符的最长有效对和当前`)`与以`s[i-1]`结尾的最长有效括号对的上一个位置的`(`后，之前的最长有效对数。

```java
class Solution {
    public int longestValidParentheses(String s) {
        if(s == null || s.length() == 0)
            return 0;
        int maxans = 0;
        int dp[] = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxans = Math.max(maxans, dp[i]);
            }
        }
        return maxans;
    }
}
```

#### 复杂度分析:

- **时间复杂度**：$O(n)$
- **空间复杂度：**$O(n)$

