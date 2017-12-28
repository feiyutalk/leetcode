# 520. Detect Capital

```java
class Solution {
    public boolean detectCapitalUse(String word) {
        if(word == null || word.length() == 0)
            return true;
        //case 1 all capitals
        boolean allCapitals = true;
        for(Character c : word.toCharArray()){
            if(!(c >= 'A' && c <= 'Z')){
                allCapitals = false;
                break;
            }
        }
        if(allCapitals) return true;
        //case 2 all not capitals
        boolean allNotCapitals = true;
        for(Character c : word.toCharArray()){
            if(!(c >= 'a' && c <= 'z')){
                allNotCapitals = false;
                break;
            }
        }
        if(allNotCapitals) return true;
        //case 3 first Capitals
        if(!(word.charAt(0) >= 'A' && word.charAt(0) <= 'Z')) return false;
        boolean firstCapital = true;
        for(int i=1; i<word.length(); i++){
            if(!(word.charAt(i) >= 'a' && word.charAt(i) <= 'z')){
                firstCapital = false;
                break;
            }
        }
        if(firstCapital) return true;
        return false;
    }
}
```

