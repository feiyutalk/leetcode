# Description

:star2::star2:

![](/images/SubsetsII.png)

***
## Analysis
这道题目还是递归的问题，求解集合的问题难点，在于如何去掉重复计算，去掉重复计算的方法在于如果相邻两个是一样的元素，比如 ..2, 2... 那么(选,不选) (不选,选) 这样的情况下是有重复的，我们只要在算法中过滤掉这两种情况中的一种情况就可以了。递归的模板没有变化。我们必须往递归的结构上去构造，包括此题的先排序，以及定义choose数组。
## Solution 递归求解+去重技巧

```java
public class Solution {
    static List<List<Integer>> ans = new ArrayList<List<Integer>>();
    static boolean[] choose;
    
    public void recur(int idx, int[] nums){
        if(idx >= nums.length){
            ArrayList<Integer> temp = new ArrayList<Integer>();
            for(int i=0;i<choose.length;i++){
                if(choose[i])
                    temp.add(nums[i]);
            }
            ans.add(temp);
            return;
        }
        
        if(idx > 0 && nums[idx-1] == nums[idx] && choose[idx-1] == false){
            choose[idx] = false;
            recur(idx+1, nums);
        }else{
            choose[idx] = true;
            recur(idx+1, nums);
            choose[idx] = false;
            recur(idx+1, nums);
        }
    }
    
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        ans.clear();
        choose = new boolean[nums.length];
        for(int i=0; i<nums.length;i++){
             int k = i;
            for(int j=i+1; j<nums.length; j++){
                if(nums[j] < nums[k])
                    k = j;
            }
            if(k != i){
                int temp  = nums[i];
                nums[i] = nums[k];
                nums[k] = temp;
            }
        }
        recur(0, nums);
        return ans;
    }
}
```
***
enjoy life, coding now! :D
ow! :D
