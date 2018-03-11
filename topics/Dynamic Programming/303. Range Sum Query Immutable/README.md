# 303. Range Sum Query - Immutable
## #1 暴力求解[TLE]
遍历指定的范围，然后累加求和。 


```Java
public class NumArray {
  int[] nums;
  public NumArray(int[] nums) {
    this.nums = nums;
  }

  public int sumRange(int i, int j) {
    int result = 0;
    for(int k=i; k<=j; k++)
      result+=nums[k];
    return result;
  }
}
```


我们结果是对，但是呢，却超时了。我们的时间复杂度只是O(n)，在这种情况下还出现了 超时，那么说明，我们需要一种O(1)时间复杂度的算法。要达到O(1)的时间复杂度，必须依赖于已经构建好的数据结构！这道题目中nums中存放的是元素的值，但是呢，我们所要得到是什么呢？我们需要的实际是范围和，所以，我们希望将存放元素值的数据结构转化为存放范围和的数据结构。

## #2 累加数组[AC]
建立存放范围和的数据结构。

```Java
public class NumArray {
    int[] nums;
    public NumArray(int[] nums) {
       for(int i=1;i<nums.length; i++)
           nums[i]+=nums[i-1];
        this.nums = nums;
    }
    
    public int sumRange(int i, int j) {
       if(i == 0)
           return nums[j];
        return nums[j] - nums[i-1];
    }

}
/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```

那么在构建的时候，时间复杂度为O(n)，但是在每次求范围和的时候，时间复杂度为O(1)。所以，有时候，我们再做算法题时候，不旦旦只是要在时间和空间中去做一个权衡，还需要考虑在构建数据结构和使用数据结构之中做权衡。
