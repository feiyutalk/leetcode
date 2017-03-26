# Description

:star2::star2:

![](/images/Combination_Sum.png)

***
## Analysis
递归递归递归递归。。。。。被这道题卡了半个多小时，问题在于，对递归的理解有一个思维定势，总认为，递归调用，问题规模要减少，但是这道题，元素是可以重复出现了，如果递归调用时减少了数组的长度，那么就得到不到元素重复出现的解，其实这道题目递归调用时，只要减少target的值就可以了。

## Solution 递归求解

```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        List<Integer> a = new ArrayList<Integer>();
        recCombinationSum(ans, a, candidates, candidates.length-1,target);
        return ans;
    }
    
    public void recCombinationSum(List<List<Integer>> ans, List<Integer> a, int[] candidates, int length, int target){
        if(target < 0){
            return ;
        }
        
        if(target == 0){
            ans.add(new ArrayList(a));
            return ;
        }
        
        for(int i=length; i>=0; i--){
            a.add(candidates[i]);
            recCombinationSum(ans, a, candidates, i, target-candidates[i]);
            a.remove(new Integer(candidates[i]));
        }
    }
}
```
***
enjoy life, coding now! :Dnt n, int k){
        
        if(k == 0){
            ans.add(new ArrayList(a));
            return;
        }
        
        for(int i=n; i>=1; i--){
            a.add(i);
            recCombine(ans, a, i-1, k-1);
            a.remove(new Integer(i));
        }
    }
}
```
***
enjoy life, coding now! :D