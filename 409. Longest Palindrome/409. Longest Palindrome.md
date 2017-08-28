# 409. Longest Palindrome
## Description

```
Difficulty: Easy
```

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:

	Input:
	"abccccdd"
	
	Output:
	7
	
	Explanation:
	One longest palindrome that can be built is "dccaccd", whose length is 7.
## Solution 1
首先，这题目只关心回文串的长度，而不关系里面字符具体如何排序。所有，我们只要知道字符的个数就可以了，因为只有字符的个数取偶数个，才能放到回文串中，所以，问题就转化为，我们要统计每个字符及其出现的个数。我们需要把传入的string这个类型转为为HashMap，Key是字符，Value是其出现的个数。只要把该数据结构构建出来，那么算法是非常简单的。

做完这道题目，我们应该总结出来，统计每个元素统计信息的的方法：

1. 构造一个HashMap
2. 以元素值作为Key，其统计信息作为Value。

```java

class Solution {
    public int longestPalindrome(String s) {
        //I
        if(s == null || s.length() == 0)
            return 0;
        //II
        boolean one = false;
        int result = 0;
        // 1. new map
        Map<Character, Integer> map = new HashMap<>();
        // 2. construct map
        for(Character c : s.toCharArray()){
            map.put(c, map.getOrDefault(c,0)+1);
        }
        for(Map.Entry<Character, Integer> entry : map.entrySet()){
            result += entry.getValue()/2;
            if(!one){
                one = entry.getValue()%2 == 1;
            }
        }
        return 2 * result + (one == true?1:0);
    }
}
```

***

**enjoy life, coding now! :D**
