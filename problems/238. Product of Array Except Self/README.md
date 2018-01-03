# 238. Product of Array Except Self

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        if(nums == null || nums.length == 0)
            return nums;
        int[] res = new int[nums.length];
        List<Integer> set = new ArrayList<>();
        int mulRes = 1;
        for(int i=0; i<nums.length; i++){
            if(nums[i] == 0){
                set.add(i);
                continue;
            }
            mulRes *= nums[i];
        }
        if(set.size() == 0){
            for(int i=0; i<nums.length; i++){
                res[i] = mulRes/nums[i];
            }
            return res;
        }else if(set.size() == 1){
            int zIdx = set.get(0);
            for(int i=0; i<nums.length; i++){
                if(i != zIdx){
                    res[i] = 0;
                }else{
                    res[i] = mulRes;
                }
            }
            return res;
        }else{
            for(int i=0; i<nums.length; i++)
                res[i] = 0;
            return res;
        }
    }
}
```

