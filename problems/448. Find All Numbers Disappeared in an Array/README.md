# #1 Set[AC]

## 思路

我们通过`HashSet`这种数据结构来记录$1-n$在`nums`已经出现过的元素，然后将没出现过的元素返回。

## 算法

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        Set<Integer> appear = new HashSet<>();
        for(int num : nums)
            appear.add(num);
        for(int i=1; i<=nums.length; i++)
            if(!appear.contains(i))
                res.add(i);
        return res;
    }
}
```

## 性能分析

### 时间复杂度
$O(n)$

### 空间复杂度
$O(n)$

# #2 标记法[AC]

## 思路

由于数组中的元素值满足：$1\leq nums[i]\leq n$，因此$0\leq nums[i]-1\leq n-1$，这意味着我们可以把$nums[i]-1$当做数组的下标索引。因此，我们只需要判断该索引是否出现过即可，如何判断呢？我们把$nums[nums[i]-1]$当做判别标记。

![](http://p6sh0jwf6.bkt.clouddn.com/2018-10-19-%E6%A0%87%E8%AE%B0%E6%B3%95.gif)

## 算法

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        for(int i=0; i<nums.length; i++){
            int idx = Math.abs(nums[i])-1;
            if(nums[idx] > 0)
                nums[idx] = -nums[idx];
        }
        for(int i=1; i<=nums.length; i++)
            if(nums[i-1] > 0)
                res.add(i);
        return res;
    }
}
```

## 性能分析

### 时间复杂度
$O(n)$

### 空间复杂度
$O(n)$