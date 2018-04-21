# 171. Excel Sheet Column Number

## #1 乘膜累加[AC]

### 算法

```java
class Solution {
    public int titleToNumber(String s) {
        if(s == null || s.length() == 0)
            return 0;
        int power = 1;
        int res = 0;
        for(int i=s.length()-1; i>=0; i--){
            res += ((s.charAt(i) - 'A' + 1)*power);
            power *= 26;
        }
        return res;
    }
}
```

