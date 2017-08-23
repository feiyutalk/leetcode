# 219. Contains Duplicate II
## Description

```
Difficulty: Easy
```

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

## Solution 1 时空互换
  可以考虑用二重循环来处理，但是时间复杂度会比较高，为 $$O(n^2)$$,我们当然可以用时空互换的方式，用一个map来存储元素，使得判断两个元素是否相等的时间复杂度为O(1)进而，使得整个算法的时间复杂度为O(n)，但是空间复杂度也为O(n)。

```java

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if(nums == null || nums.length == 0 || k <0)
            return false;
        
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<nums.length; i++){
            if(map.containsKey(nums[i])){//exist same value
                int index = map.get(nums[i]);
                if(i-index<=k)
                    return true;
            }
            map.put(nums[i], i);
        }
        return false;
    }
}
```

***

**enjoy life, coding now! :D**
