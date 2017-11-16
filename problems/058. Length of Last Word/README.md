# 058. Length of Last Word

# Solution

这种题目符合简单题目的特点，就是线性遍历+统计因子。这道题目要统计的是什么呢？统计最后一个单词的字符数，单词之间用空格隔开。实际上非常的简单，主要用一个统计变量遇到字符就加1，遇到空格就置零就可以解决了，但是这道题目的边界条件比较烦的一点就是像`"a "`这个输入，就会导致我们上面的算法出错，所以，在进入线性遍历之前要先把最后的空格都过滤掉。

```java
class Solution {
    public int lengthOfLastWord(String s) {
        //boundary condition
        if(s == null || s.length() == 0)
            return 0;
        //normal condition
        int size = s.length();
        while(s.charAt(size-1) == ' '){
            size--;
            if(size == 0) return 0;
        }
        int count = 0;
        for(int i=0; i<size; i++){
            if(s.charAt(i) != ' ') count++;
            else count = 0;
        }
        return count;
    }
}
```

