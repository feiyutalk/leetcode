# 318. Maximum Product of Word Lengths
## #1 暴力求解法[TLE]
### 思路

我们采用暴力搜索的方式，遍历所有可能的单词对，然后判断两个单词对之间是否有相同的字符，如果没有相同的字符，就将它们的长度之积和最终结果做比较。

### 算法

```java

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
```

### 复杂度分析

- 时间复杂度：$O(n^4)$
- 空间复杂度：$O(1)$

这个算法在LeetCode提交的时候出现了超时，这个算法的时间复杂度为$O(n^4)$，显然需要优化。优化的角度在哪里呢？我们的算法中`containsCL()`的复杂度是$O(n^2)$，需要被执行$O(n^2)$次，所以我们优化的角度要么在`containsCL()`这个子算法中，要么在操作执行次数上。我们发现，要求出两个字符串长度乘积的最大值，那么二重循环可能避免不了，所以我们把注意力放在判断两个字符串是否有公共的字符的子算法中！

那么要判断两个字符串是否有公共的字符，怎么也要遍历每个字符吧，这样也避免不了二重循环的！！那么怎么优化呢？这时候我们想办法去构造一个新的数据结构，想办法做到在初始化和操作之间做权衡！我们希望containsCL()是借助一个新的数据结构来求解的，求解时的时间复杂度能达到O(1)，把`O(n^2)`的时间复杂度转化到构造这个新的数据结构上！

## #2 bitmap位图[AC]
### 思路

我们可以通过位图的方式来存储字符串，但是这个有一个缺点，只能做到存储字符串中存在的字符，不能记住字符出现的次序，忽略掉了字符之间的关系。这种数据结构能用在什么地方呢？恰恰能用在判断两个字符串**是否包含共同的字符**，因为这个问题，它只关系字符是否出现，本身就忽视了字符之间的关系。

**位图原理**如下: 

![bitmap原理](http://p6sh0jwf6.bkt.clouddn.com/2018-04-12-112850.jpg)

现在的主要问题是，如果构造这个位图。想法是这样的，我们利用`current_char - 'a'`的值来判断当前字符是哪个字符，并利用该差值确定存储该字符的位置：

- `'a' - 'a' = 0`所以，a会放到第0位，对应的从右往左的移位数为0；
- `'b' - 'a' = 1`所以，b会放到第1位，对应的从右往左的移位数为1；
- ...
- `'z' - 'a' = 25`所以，z会放到第25位，对应的从右往左的移位数为25；

通过上面的观察，我们可以发现，利用 `bitmap |= (1 << (words.charAt(i) - 'a'))`可以实现单词变bitmap。

### 算法

```java
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
### 复杂度分析

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$

