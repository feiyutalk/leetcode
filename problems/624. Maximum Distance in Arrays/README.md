# 611. Valid Triangle Number

```java
class Solution {
    public int maxDistance(List<List<Integer>> arrays) {
        if(arrays == null && arrays.size() == 0)
            return 0;
        //find min
        int min = Integer.MAX_VALUE;
        int mIdx = 0;
        for(int i=0; i<arrays.size(); i++){
            if(arrays.get(i).get(0) < min){
                min = arrays.get(i).get(0);
                mIdx = i;
            }
        }
        //find max
        int max = Integer.MIN_VALUE;
        for(int i=0; i<arrays.size(); i++){
            if(arrays.get(i).get(arrays.get(i).size()-1) > max && i != mIdx){
                max = arrays.get(i).get(arrays.get(i).size()-1);
            }
        }
        int res1 = Math.abs(max - min);
        
        //find max
        max = Integer.MIN_VALUE;
        mIdx = 0;
        for(int i=0; i<arrays.size(); i++){
            if(arrays.get(i).get(arrays.get(i).size()-1) > max){
                max = arrays.get(i).get(arrays.get(i).size()-1);
                mIdx = i;
            }
        }
        //find min
        min = Integer.MAX_VALUE;
        for(int i=0; i<arrays.size(); i++){
            if(arrays.get(i).get(0) < min && i != mIdx){
                min = arrays.get(i).get(0);
            }
        }
        int res2 = Math.abs(max - min);
        return res1 > res2?res1 : res2;
    }
}
```



