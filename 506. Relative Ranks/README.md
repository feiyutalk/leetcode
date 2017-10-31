# 506. Relative Ranks

# Description

Given scores of **N** athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".

**Example 1:**

```
Input: [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal". 
For the left two athletes, you just need to output their relative ranks according to their scores.
```

# Solution

这道题目，最重要的是需要对分数降序排序，这样的话，我们就把前三个分数的对应的位置存入字符串 "Gold Medal", "Silver Medal" and "Bronze Medal"，然后将其他位置存入对应排名的字符串。但是当我们拿原来数组进行排序的时候，元素的位置就发生变化了，我们就不知道之前元素所在的位置是哪了。所以，我们需要记录下排序之前的元素的位置，我这里采用HashMap来存储每个元素对应的位置的，因为题目说了，每个分数是唯一的，没有重复的分数，所以可以将分数作为键，下标作为值。最后，我们排序后，就可以找到该分数对应的位置替换成对应名次的字符串就可以了。

```java
class Solution {
    public String[] findRelativeRanks(int[] nums) {
        //boundary condition
        if(nums == null || nums.length == 0)
            return new String[0];
        //normal condition
        String[] result = new String[nums.length];
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<nums.length; i++){
            map.put(nums[i], i);
        }
        Arrays.sort(nums);
        for(int i=nums.length-1; i>=0; i--){
            if(i == nums.length-1){
                result[map.get(nums[i])] = "Gold Medal";
            }else if(i == nums.length-2){
                result[map.get(nums[i])] = "Silver Medal";
            }else if(i == nums.length-3){
                result[map.get(nums[i])] = "Bronze Medal";
            }else{
                result[map.get(nums[i])] = nums.length - i + "";
            }
        }
        return result;
    }
}
```

