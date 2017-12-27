# 611. Valid Triangle Number

TLE

```java
class Solution {
    private int res = 0;
    public int triangleNumber(int[] nums) {
        if(nums.length < 3) return 0;
        Arrays.sort(nums);
        backtrack(nums, new ArrayList<Integer>(), 0);
        return res;
    }
    
    private void backtrack(int[] nums, List<Integer> temp, int step){
        if(temp.size() == 3){
            if(isTriangleNumber(temp)){
                res++;
            }
        }
        
        for(int i=step; i<nums.length; i++){
            temp.add(nums[i]);
            backtrack(nums, temp, i+1);
            temp.remove(temp.size()-1);
        }
    }
    
    private boolean isTriangleNumber(List<Integer> sides){
        return sides.get(0) + sides.get(1) > sides.get(2) &&
               sides.get(0) + sides.get(2) > sides.get(1) &&
               sides.get(1) + sides.get(2) > sides.get(0);
    }
}
```

AC

```java

```

