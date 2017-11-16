# 5. Longest Palindromic Substring
## Description

```
Difficulty: Medium
```
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:

	Input: "babad"
	
	Output: "bab"
	
	Note: "aba" is also a valid answer.

Example:

	Input: "cbbd"
	
	Output: "bb"
## Solution 1
由于回文串的特殊性，它的主要矛盾点在于回文串是关于中心点对称的，但是存在两种情况

1. aba 这种有中心元素的
2. bb 这种没有中心元素的

那么，我们在设计算法的时候，我们可以遍历字符串里面的每个字符，然后考虑以该字符作为中心元素，或者最靠近中心点的元素来枚举出以该元素为中心可能的最长的回文子串。这样的时间复杂为 O(n^2), 这在字符串子串问题里面是可以接受的。

接触了不少的回文串的问题了，我们可以总结一下回文串的一般规律:

1. 关于中心点（这里的中心点不一定指中心元素）的其他元素是对称的，这就意味着他们的统计信息（个数）都是偶数，当然排除中心元素外。
2. 考虑回文串的时候要分两种情况，一是有中心元素的如 aba， 二是没有中心元素的 如 bb
3. 一般回文串的算法都要设置两个指针，做对称位置的元素判断。


```java

class Solution {
    public String longestPalindrome(String s) {
        // I
        if(s == null || s.length() == 0)
            return "";
        if(s.length() == 1)
            return s;
        
        //II
        int low = 0;
        int maxLen = 1;
        for(int i=0; i<s.length()-1; i++){
            if(i-1>=0 && s.charAt(i-1) == s.charAt(i+1)){
                int j = i-1;
                int k = i+1;
                while(j>=0&&k<s.length()&&s.charAt(j)==s.charAt(k)){
                    j--;
                    k++;
                }
                if(maxLen < k-j-1){
                    maxLen = k - j -1;
                    low = j + 1;
                }
            }
            if(s.charAt(i) == s.charAt(i+1)){
                int j = i;
                int k = i+1;
                 while(j>=0&&k<s.length()&&s.charAt(j)==s.charAt(k)){
                    j--;
                    k++;
                }
                if(maxLen < k-j-1){
                    maxLen = k - j -1;
                    low = j + 1;
                }
            }
        }
        return s.substring(low, low + maxLen);
    }
}
```

***

**enjoy life, coding now! :D**
