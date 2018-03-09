# 120. Triangle

## #1 动态规划[AC]

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int[] res = new int[triangle.size() + 1];
        for(int i=triangle.size()-1; i>=0; i--){
            for(int j=0; j<triangle.get(i).size(); j++){
                res[j] = Math.min(res[j], res[j+1]) + triangle.get(i).get(j);
            }
        }
        return res[0];
    }
}
```

