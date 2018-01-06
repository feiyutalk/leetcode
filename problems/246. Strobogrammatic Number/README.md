# 246. Strobogrammatic Number

```java
class Solution {
    public boolean isStrobogrammatic(String num) {
        // 0 1 2 3 4 5 6 7 8 9
        // 只有 0 1 8 以及 6 9 满足翻转对称性
        // 偶数 1 2 3 4  奇数 1 2 3 4 5 还需要多一步判断
        if(num == null || num.length() == 0)
            return true;
        int i = 0, j = num.length()-1;
        for(; i<j; i++,j--){
            if(num.charAt(i) != num.charAt(j)){
                if(!((num.charAt(i) == '6' && num.charAt(j) == '9') || (num.charAt(i) == '9' && num.charAt(j) == '6'))){
                    return false;
                }
            }else{
                if(num.charAt(i) != '0' && num.charAt(i) != '1' && num.charAt(i) != '8'){
                    return false;
                }
            }
        }
        if(num.length() % 2 == 1)
            if(num.charAt(i) != '0' && num.charAt(i) != '1' && num.charAt(i) != '8')
                return false;
        return true;
    }
}
```

