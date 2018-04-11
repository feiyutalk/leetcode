# 268. Missing Number

## #1 等差数组求和公式[AC]

### 思路

我们利用一个特性，就是$sum = 0+1+2+…+n = \frac{n(n+1)}{2}$，如果里面有一个值（不妨设为m）丢失，那最后得到的求和结果就是$sum\_miss = \frac{n(n+1)}{2}-m$。所以，我们简单的就是公式变换，就可以得到$m$的值了。

### 算法

```java
class Solution {
    public int missingNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        int n = nums.length;
        int sum = n*(n+1)/2;
        for(int num : nums)
            sum -= num;
        return sum;
    }
}
```

### 复杂度分析

- **时间复杂度**：$O(n)$
- **空间复杂度**：$O(1)$

## #2 排序[AC]

### 思路

先对数组进行排序，如果数组中没有数据丢失，那么对于每个元素，必然满足`nums[i] = nums[i-1]+1`（除了第一个元素外），因为有元素丢失，所以这个性质被破坏，我们只需要找出在哪个元素破坏了上面这个性质即可。

### 算法

```java
class Solution {
    public int missingNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        Arrays.sort(nums);
        if(nums[0] != 0)
            return 0;
        for(int i=1; i<nums.length; i++){
            if(nums[i] != nums[i-1]+1)
                return nums[i-1]+1;
        }
        return nums.length;
    }
}
```

### 复杂度分析

- 时间复杂度**：$O(nlogn)$
- **空间复杂度**：$O(1)$

## #3 位操作[AC]

### 思路

位操作是利用XOR（异或）这个运算特性来做的，在[Single Number](https://leetcode.com/problems/single-number)、[Single Number III](https://leetcode.com/problems/single-number-iii)的题目中，我们利用XOR操作来找到数组中只出现一次的元素（其他元素都出现两次），那么对于这道题目我们是否也可以这样做的。乍一看，数组似乎就没有重复的元素嘛，但是我们如果把数组的`index`和数组的最大值加上，就会出现缺失值只出现一次，其他元素出现两次这样的数组了，非常的巧妙。

**Miss = 4**

| Index | 0    | 1    | 2    | 3    |
| ----- | ---- | ---- | ---- | ---- |
| Value | 0    | 1    | 3    | 4    |

我们得到的数组为：`[0,0,1,1,2,3,3,4]`，然后只出现一次的2就是我们要找的答案了。

### 算法

```java
class Solution {
    public int missingNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        int miss = nums.length;
        for(int i=0; i<nums.length; i++){
            miss ^= i;
            miss ^= nums[i];
        }
        return miss;
    }
}
```

### 复杂度分析

- **时间复杂度**：$O(n)$
- **空间复杂度**：$O(1)$

