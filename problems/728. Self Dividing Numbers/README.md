# 728. Self Dividing Numbers

```java
class Solution {
    public List<Integer> selfDividingNumbers(int left, int right) {
        if(left > right)
            return new ArrayList<Integer>();
        List<Integer> res = new ArrayList<>();
        for(int i=left; i<=right; i++){
            if(isSDNumber(i))
                res.add(i);
        }
        return res;
    }
    
    private List<Integer> getDigits(int num){
        List<Integer> res = new ArrayList<>();
        while(num != 0){
            res.add(num % 10);
            num /= 10;
        }
        return res;
    }
    
    private boolean isSDNumber(int num){
        List<Integer> digits = getDigits(num);
        if(digits.contains(0)) return false;
        for(int digit : digits){
            if(num % digit != 0)
                return false;
        }
        return true;
    }
}
```

