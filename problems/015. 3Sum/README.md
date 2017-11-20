# 015. 3Sum

使用`Two points`的解题模板来求解，固定一个变量，转化为`two points`的问题。

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if(nums == null || nums.length == 0)
            return new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        for(int i=0; i<nums.length; i++){
            if(i == 0 || nums[i] != nums[i-1]){
                int l = i+1;
                int r = nums.length - 1;
                while(l<r){
                    if(nums[i] + nums[l] + nums[r] == 0){
                        result.add(Arrays.asList(new Integer[]{nums[i], nums[l], nums[r]}));
                        while(l<r && nums[l] == nums[l+1]){
                            l += 1;
                        }
                        while(l<r && nums[r] == nums[r-1]){
                            r -= 1;
                        }
                        l += 1;
                        r -= 1;
                    }else if(nums[i] + nums[l] + nums[r] < 0){
                        l += 1;
                    }else{
                        r -= 1;
                    }
                }
            }
        }
        return result;
    }
}
```

