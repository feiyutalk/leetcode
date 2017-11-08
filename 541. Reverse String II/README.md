# 541. Reverse String II

# Solution

这道题目需要翻转字符串，但是加了限制条件，这个限制条件就是:

- 翻转指定字符串指定区间中的字符

这边封装了一个函数用于处理字符串指定区间中的字符翻转。其他的并没有什么特别的。

```java
class Solution {
    public String reverseStr(String s, int k) {
        //boundary condition
        if(s == null || s.length() == 0)
            return s;
        if(k>s.length())
            return new String(reverse(s.toCharArray(), 0, s.length()-1));
        //normal condition
        char[] chars = s.toCharArray();
        for(int i=0; i<s.length(); i+=(2*k)){
            int high = Math.min(i+k-1, s.length()-1);
            reverse(chars, i, high);
        }
        return new String(chars);
    }
    
    private char[] reverse(char[] chars, int low, int high){
        while(low<high){
            char temp = chars[low];
            chars[low] = chars[high];
            chars[high] = temp;
            low++;
            high--;
        }
        return chars;
    }
}
```

