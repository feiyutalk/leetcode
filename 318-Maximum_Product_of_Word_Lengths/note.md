# 318. Maximum Product of Word Lengths
## Description

```
Difficulty: Easy
```

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

**Example 1:**

Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]

Return 16

The two words can be "abcw", "xtfn".

**Example 2:**

Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]

Return 4

The two words can be "ab", "cd".

**Example 3:**

Given ["a", "aa", "aaa", "aaaa"]

Return 0

No such pair of words.
## Solution 1 暴力求解法
  这道题目涉及两个子算法，第一个是需要去判断两个字符串是否包含有共同的字符。第二个子算法，是选出没有包含公共字符并且字符串长度乘积之和最大。

	class Solution {
	    public int maxProduct(String[] words) {
	        if(words == null || words.length == 0)
	            return 0;
	        int result = 0;
	        for(int i=0; i<words.length-1; i++){
	            for(int j=0; j<words.length; j++){
	                if(!containsCL(words[i], words[j])){
	                    result = Math.max(result, words[i].length()*words[j].length());
	                }
	            }
	        }
	        return result;
	    }
	    
	    public boolean containsCL(String word1, String word2){
	        for(Character c1 : word1.toCharArray()){
	            for(Character c2 : word2.toCharArray()){
	                if(c1 == c2)
	                    return true;
	            }
	        }
	        return false;
	    }
	}

这个算法在LeetCode提交的时候出现了超时，这个算法的时间复杂度为O(n^4),显然需要优化。优化的角度在哪里呢？我们的算法中containsCL()的复杂度是O(n^2)，需要被执行O(n^2)次，所有我们优化的角度要么在containsCL()这个子算法中，要么在操作的个数上。我们发现，要求出两个字符串长度乘积的最大值，那么二重循环可能避免不了，所以我们把注意力放在判断两个字符串是否有公共的字符的子算法中！

那么要判断两个字符串是否有公共的字符，怎么也要遍历每个字符吧，这样也避免不了二重循环的！！那么怎么优化呢？这时候我们想办法去构造一个新的数据结构，想办法做到在初始化和操作之间做权衡！我们希望containsCL()是借助一个新的数据结构来求解的，求解时的时间复杂度能达到O(1)，把O(n^2)的时间复杂度转化到构造这个新的数据结构上！

## Solution 2 bitmap
  我们可以通过位图的方式来存储字符串，但是这个有一个缺点，只能做到存储字符串中存在的字符，不能记住字符出现的次序，忽略掉了字符之间的关系。这种数据结构能用在什么地方呢？恰恰能用在判断两个字符串是否包含共同的字符，因为这个问题，它只关系字符是否出现，本身就忽视了字符之间的关系。

  **位图原理**如下:
![](/318-Maximum_Product_of_Word_Lengths/bitmap原理.png)

```

class Solution {
    public int maxProduct(String[] words) {
	if(words == null || words.length == 0)
	    return 0;
	int result = 0;
	int[] bitmap = new int[words.length];

	//initialize bitmap
	for(int i=0; i<words.length; i++){
	    for(int j=0; j<words[i].length(); j++){
		bitmap[i] |= (1<<(words[i].charAt(j) - 'a'));
	    }
	}

	for(int i=0; i<words.length-1; i++){
	    for(int j=i+1; j<words.length; j++){
		if((bitmap[i] & bitmap[j]) == 0){
		    result = Math.max(result, words[i].length() * words[j].length());
		} 
	    }
	}
	return result;
    }
}

```
***

**enjoy life, coding now! :D**
