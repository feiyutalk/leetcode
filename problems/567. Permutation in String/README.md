# 567. Permutation in String

这道题目是属于`Two points`中的滑动窗口问题，我们需要判断s2中是否包含s1中所以字符排列中的任意一个，实际上只需要判断是否s1中的每个字符也在s2中，所以我们可以把s1中的所有排列字符串抽象成一个映射(Character -> Count)，只需要统计s1中的元素个数就可以了。

然后，我们用一个s1字符串大小的窗口在s2中向右滑动，移出一个字符的时候就减掉该字符count，移入一个字符就加上该字符count。

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if(s1 == null || s1.length() == 0)
            return true;
        if(s2 == null || s2.length() == 0)
            return false;
        if(s1.length() > s2.length())
            return false;
        
        int[] count = new int[26];
        for(int i=0; i<s1.length(); i++){
            count[s1.charAt(i) - 'a']++;
            count[s2.charAt(i) - 'a']--;
        }
        if(allZeros(count)) return true;
        for(int i=s1.length(); i<s2.length(); i++){
            count[s2.charAt(i) - 'a']--;
            count[s2.charAt(i-s1.length()) - 'a']++;
            if(allZeros(count)) return true;
        }
        return false;
    }
    
    private boolean allZeros(int[] count){
        for(int num : count){
            if(num != 0)
                return false;
        }
        return true;
    } 
}
```

