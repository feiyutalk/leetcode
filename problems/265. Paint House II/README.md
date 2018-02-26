# 265. Paint House II

## \#1 暴力搜索[TLE]

这个解法思路比较简单，就是去遍历每个房子可能的涂色的方案，最后穷举了所有可能的涂色的方案，然后记录下所有涂色方案中，成本开销最小的值。这个方法思路简单、直接，通过递归的方式实现，但是时间复杂度为$O(k^n)$，时间复杂度较高，最后提交的时候超时。

```java
class Solution {
    private int res = Integer.MAX_VALUE;
    
    public int minCostII(int[][] costs) {
        if(costs == null || costs.length == 0)
            return 0;
        helper(new ArrayList<Integer>(), costs, 0, -1);
        return res;
    }
    
    private void helper(List<Integer> temp, int[][] costs, int step, int used){
        if(temp.size() == costs.length){
            res = Math.min(res, sum(temp));
            return;
        }
        for(int i=0; i<costs[0].length; i++){
            if(i == used)
                continue;
            temp.add(costs[step][i]);
            helper(temp, costs, step+1, i);
            temp.remove(temp.size()-1);
        }
    }
    
    private int sum(List<Integer> nums){
        int res = 0;
        for(int num : nums)
            res += num;
        return res;
    }
}
```



