# 016. 3Sum Closest

还是转换为`two points` 来求解。

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if(nums == null || nums.length < 3)
            return 0;
        
        Arrays.sort(nums);
        long res = Integer.MAX_VALUE;
        long ltarget = (long)target;
        
        for(int i=0; i<nums.length; i++){
            int l = i+1;
            int r = nums.length -1;
            while(l<r){
                long temp = nums[i] + nums[l] + nums[r];
                if(Math.abs(temp - ltarget) < Math.abs(res - ltarget))
                    res = temp;
                if(temp == ltarget)
                    return (int)temp;
                else if(temp < ltarget)
                    l += 1;
                else
                    r -= 1;
            }
        }
        return (int)res;
    }
}
```

