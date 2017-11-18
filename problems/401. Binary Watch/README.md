# 401. Binary Watch

```java
class Solution {
    public List<String> readBinaryWatch(int num) {
        if(num <= 0) return new ArrayList<String>();
        ArrayList<String> result = new ArrayList<>();
        for(int i=0; i<12; i++){
            for(int j=0; j<60; j++){
                if(Integer.bitCount(i) + Integer.bitCount(j) == num){
                    result.add(String.format("%d:%02d", i, j));
                }
            }
        }
        return result;
    }
}
```

