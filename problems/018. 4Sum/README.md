# 018. 4Sum

这道题目可以先转换为3Sum,然后用`two poins`的方式来求解。

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        if(nums == null || nums.length < 4)
            return new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        ArrayList<List<Integer>> res = new ArrayList<>();
        for(int i=0; i<nums.length-3; i++){
            if(nums[i]+nums[i+1]+nums[i+2]+nums[i+3] > target) break;
            if(nums[i]+nums[nums.length-1]+nums[nums.length-2]+nums[nums.length-3] < target) continue;
            if(i>0 && nums[i] == nums[i-1]) continue;
            for(int j=i+1; j<nums.length-2; j++){
                if(nums[i]+nums[j]+nums[j+1]+nums[j+2]>target)break;
                if(nums[i]+nums[j]+nums[nums.length-1]+nums[nums.length-2]<target)continue;
                if(j>i+1&&nums[j]==nums[j-1])continue;
                int low=j+1, high=nums.length-1;
                while(low<high){
                    int sum=nums[i]+nums[j]+nums[low]+nums[high];
                    if(sum==target){
                        res.add(Arrays.asList(nums[i], nums[j], nums[low], nums[high]));
                        while(low<high&&nums[low]==nums[low+1])low++; //skipping over duplicate on low
                        while(low<high&&nums[high]==nums[high-1])high--; //skipping over duplicate on high
                        low++; 
                        high--;
                    }
                    //move window
                    else if(sum<target)low++; 
                    else high--;
                }
            }
        }
        return res;
    }
}
```

