# 345. Reverse Vowels of a String

# Solution

这道题目，实际上就是在遍历的过程中，找到元音字符才停止，如果不是元音字母，就继续遍历。注意下标就行了。

```java
class Solution {
    public String reverseVowels(String s) {
        if(s == null || s.length() == 0)
            return s;
        StringBuffer sb = new StringBuffer(s);
        int i = 0, j = s.length()-1;
        while(i<j){
            while(i<j && !isVowel(sb.charAt(i))) i++;
            if(i >= j) return sb.toString();
            while(i<j && !isVowel(sb.charAt(j))) j--;
            if(i >= j) return sb.toString();
            char temp = sb.charAt(i);
            sb.setCharAt(i, sb.charAt(j));
            sb.setCharAt(j, temp);
            i++;
            j--;
        }
        return sb.toString();
    }
    
    private boolean isVowel(char c){
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' 
            || c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U';
    }
}
```

