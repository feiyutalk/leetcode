# 087. Scramble String

## #1 递归(AC)

要判断两个字符串是否满足`scramble`关系，有两种情况需要判断：

- 第一种情况 S1左子树 scrambel S2左子树 && S1右子树 scamble S2右子树
- 第二种情况 S1左子树 scrambel S1右子树 && S1右子树 scamble S2左子树

我们可以递归的判断以上两种情况:

```java 
class Solution {
    public boolean isScramble(String s1, String s2) {
        //递归的判断
        if(s1 == null || s2 == null || s1.length() != s2.length()) return false;
        if(s1.equals(s2)) return true;
        //写一个判断条件 来判断两个字符串的包含的字符个数一样
        int[] letters = new int[26];
        for(int i=0; i<s1.length(); i++){
            letters[s1.charAt(i) - 'a']++;
            letters[s2.charAt(i) - 'a']--;
        }
        for(int letter : letters)
            if(letter != 0) return false;
        
        for(int j=1; j<s1.length(); j++){
            //第一种情况 左 scrambel 左 && 右 scamble 右
            if(isScramble(s1.substring(0, j), s2.substring(0, j)) 
               && isScramble(s1.substring(j), s2.substring(j)))
                return true;
            //第二种情况 左 scrambel 右 && 右 scamble 左
            if(isScramble(s1.substring(0, j), s2.substring(s2.length() - j)) 
               && isScramble(s1.substring(j), s2.substring(0, s2.length() - j)))
                return true;
        }
        return false;
    }
}
```

