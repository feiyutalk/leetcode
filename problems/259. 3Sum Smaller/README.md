[TOC]

# #1 暴力搜索[AC]

## 思路

遍历所有可能的三元组`i, j, k`，对于每种可能情况，判断`nums[i] + nums[j] + nums[k] < target`是否成立，如果成立，则将其记录到结果变量中。

## 算法

```java
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        if(nums == null || nums.length < 3) return 0;
        int res = 0;
        for(int i=0; i<nums.length-2; i++){
            for(int j=i+1; j<nums.length-1; j++){
                for(int k=j+1; k<nums.length; k++)
                    if(nums[i] + nums[j] + nums[k] < target)
                        res++;
            }
        }
        return res;
    }
}
```

## 性能分析

### 时间复杂度

算法中需要三重循环遍历，故时间复杂度为$O(n^3)$

### 空间复杂度

算法使用了常数个辅助变量，故空间复杂度为$O(1)$

# #2 二分搜索[AC]

## 思路

在解这道题之前，我们可以先解决其子问题

> Given a numsnums array, find the number of index pairs $i$, $j$ with $0 \leq i\leq j\leq n$ that satisfy the condition $nums[i] + nums[j] \leq target$

我们可以对数组进行排序，然后加上一层外循环，每次循环调用一次求解子问题。而子问题的求解可以通过二分搜索方法来求解。

## 算法

```java
public int threeSumSmaller(int[] nums, int target) {
    Arrays.sort(nums);
    int sum = 0;
    for (int i = 0; i < nums.length - 2; i++) {
        sum += twoSumSmaller(nums, i + 1, target - nums[i]);
    }
    return sum;
}

private int twoSumSmaller(int[] nums, int startIndex, int target) {
    int sum = 0;
    for (int i = startIndex; i < nums.length - 1; i++) {
        int j = binarySearch(nums, i, target - nums[i]);
        sum += j - i;
    }
    return sum;
}

private int binarySearch(int[] nums, int startIndex, int target) {
    int left = startIndex;
    int right = nums.length - 1;
    while (left < right) {
        int mid = (left + right + 1) / 2;
        if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid - 1;
        }
    }
    return left;
}

```

## 性能分析

### 时间复杂度

二分搜索的时间复杂度为$O(logn)$，子问题`twoSumSmaller`的时间复杂度为$O(nlogn)$，原问题`threeSumSmaller`的时间复杂度为$O(n^2logn)$

### 空间复杂度

额外空间复杂度为$O(1)$

# #3 双指针法[AC]

## 思路

我先对数组进行排序，例如，对于$nums=[3,5,2,7,1]$，排序后得$[1,2,3,5,8]$
然后，我们在该数组中查找小于$7$的三元组。

```
[1, 2, 3, 5, 8]
 ↑           ↑
left       right
```

然后，我们设置两个指针`left`和`right`，分别指向数组起始点和终止点。我们计算这两个指针指向的元素之和$sum=nums[left]+nums[right]$

- $sum > target$：这种情况说明不能包含`right`指针指向的元素，将`right`指针左移；
- $sum < target$：这种情况说明`(left, right)`满足条件，而且对于`(left, left<k<right)`的元素，也满足条件。

```java
public int threeSumSmaller(int[] nums, int target) {
    Arrays.sort(nums);
    int sum = 0;
    for (int i = 0; i < nums.length - 2; i++) {
        sum += twoSumSmaller(nums, i + 1, target - nums[i]);
    }
    return sum;
}

private int twoSumSmaller(int[] nums, int startIndex, int target) {
    int sum = 0;
    int left = startIndex;
    int right = nums.length - 1;
    while (left < right) {
        if (nums[left] + nums[right] < target) {
            sum += right - left;
            left++;
        } else {
            right--;
        }
    }
    return sum;
}
```

## 性能分析

### 时间复杂度

总的时间复杂度为$O(n^2)$

### 空间复杂度

$O(1)$