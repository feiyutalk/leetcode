# 260. Single Number III
## Description

```
Difficulty: Medium
```
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

**Note:**

1. The order of the result is not important. So in the above example, [5, 3] is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?
## Solution 1
  我们可以利用HashMap这种数据结构来记录元素及其属性，那么这道题的属性就是该元素出现的次数。当我们把这个数据结构构建起来之后，算法就简单了，只要去遍历就可以了。这样的解法时间复杂度和空间复杂度都是O(n)的。

```java

class Solution {
    public int[] singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int num : nums){
            map.put(num, map.getOrDefault(num,0)+1);
        }
        
        ArrayList<Integer> result = new ArrayList<>();
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() == 1)
                result.add(entry.getKey());
        }
        int[] arr = new int[result.size()];
        for(int i=0; i<result.size(); i++){
            arr[i] = result.get(i);
        }
        return arr;
    }
}
```

***

**enjoy life, coding now! :D**
