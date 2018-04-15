# 421. Maximum XOR of Two Numbers in an Array

## #1 暴力搜索[TLE]

### 思路

最直接的想法，就是遍历所有的可能情况，然后记录下最大的异或值。

### 算法

```java
class Solution {
    public int findMaximumXOR(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int result = 0;
        for(int i=0; i<nums.length-1; i++){
            for(int j=i+1; j<nums.length; j++)
                result = Math.max(result, nums[i] ^ nums[j]);
        }
        return result;
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

## #2 位操作[AC]

### 算法

```java
class Solution {
    public int findMaximumXOR(int[] nums) {
        int max = 0, mask = 0;
        for(int i = 31; i >= 0; i--){
            mask = mask | (1 << i);
            Set<Integer> set = new HashSet<>();
            for(int num : nums){
                set.add(num & mask);
            }
            int tmp = max | (1 << i);
            for(int prefix : set){
                if(set.contains(tmp ^ prefix)) {
                    max = tmp;
                    break;
                }
            }
        }
        return max;
    }
}
```

