# 477. Total Hamming Distance

## #1 暴力搜索+位操作[TLE]

### 思路

之前做过求解两个数Hamming Distance的题目，这个题目在数据维度进行扩展，从两个数扩展至多个数，要求这些所有的数海明距离之和。最直接的想法就是遍历所有的数值对，然后求它们的海明距离，并每个海明距离都加入到结果中。

### 算法

```java
class Solution {
    public int totalHammingDistance(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int res = 0;
        for(int i=0; i<nums.length-1; i++){
            for(int j=i+1; j<nums.length; j++)
                res += hammingDistance(nums[i], nums[j]);
        }
        return res;
    }
    
    public int hammingDistance(int x, int y) {
        return bitCount(x ^ y);
    }
    
    public int bitCount(int num){
        int count = 0;
        while(num != 0){
            num &= (num-1);
            count++;
        }
        return count;
    }
}
```

### 复杂性分析：

- 时间复杂性：$O(32*n^2)$
- 空间复杂性：$O(1)$

## #2 优化位操作[AC]

### 思路

我们可以统计在每个bit set上为1的数值个数有多少，假设统计出在第i位为1的数值个数有`k`个，那么在第i位为0的数值个数就有`n-k`个。那么第i位，对最终的海明距离的贡献值就是`k*(n-k)`。对于每个bit set，统计其贡献值，即可得到最终的结果。

### 算法

```java
class Solution {
    public int totalHammingDistance(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int n = nums.length;
        int total = 0;
        for(int i=0; i<32; i++){ // loop for all bit set
            int bitCount = 0;
            for(int j=0; j<n; j++){// loop for all number
                bitCount += (nums[j] >> i) & 1;
            }
            total += bitCount * (n - bitCount);
        }
        return total;
    }
}
```

### 复杂性分析：

- 时间复杂性：$O(n^2)$
- 空间复杂性：$O(1)$

