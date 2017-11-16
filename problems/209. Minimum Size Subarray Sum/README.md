# 209. Minimum Size Subarray Sum

# Solution

我们先将值数组转换为累加和数组，这样做的好处在于可以利用二分搜索进行求解。

对于累加和数组中的第`i`个元素，我们要做的就是求第一个大于等于`num[i]+s`的元素，这样的话，就将我们的问题转化为二分搜索的问题，属于大于等于的二分搜索题目。可以直接套用二分搜索的模板。

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int len = nums.length;
        int res = Integer.MAX_VALUE;
        int[] sub = new int[len+1];
        for(int i=1; i<len+1; i++){
            sub[i] = nums[i-1] + sub[i-1];
        }
        
        for(int i=0; i<len+1; i++){
            int l = i+1, r = len+1;
            while(l<r){
                int mid = l + (r-l)/2;
                if(sub[mid] >= sub[i] + s){
                    r = mid;
                }else{
                    l = mid + 1;
                }
            }
            if(r < len+1){
                res = Math.min(res, r-i);
            }
        }
        return (res<=len?res:0);
    }
}
```

