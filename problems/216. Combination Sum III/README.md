# 216. Combination Sum III

```java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        if(k == 0 || n <= 0) return new ArrayList<List<Integer>>();
        helper(k, n, new ArrayList<Integer>(), 1);
        return res;
    }
    
    private void helper(int k, int n, List<Integer> temp, int step){
        if(temp.size() == k){
            if(n == 0)
                res.add(new ArrayList<>(temp));
        }
        for(int i=step; i<=9; i++){
            if(n - i < 0) return;
            temp.add(i);
            helper(k, n-i, temp, i+1);
            temp.remove(temp.size()-1);
        }
    }
}
```

