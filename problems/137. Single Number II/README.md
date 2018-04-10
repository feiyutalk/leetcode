# 137. Single Number II

## #1 Hash表[AC]

通过`HashMap`这种`key-value`格式的数据结构统计列表中每个元素的个数，然后遍历`Hash表`，找出是否有`value==1`的`key`。

```java
class Solution {
    public int singleNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() == 1)
                return entry.getKey();
        }
        return -1;
    }
}
```

## #2 位操作

位操作的难度非常大，不用太纠结这种解法。

```java
class Solution {
    public int singleNumber(int[] nums) {
        int ones = 0, twos = 0;
        for(int i=0; i<nums.length; i++){
            ones = (ones ^ nums[i]) & ~twos;
            twos = (twos ^ nums[i]) & ~ones;
        }
        return ones;
    }
}
```





