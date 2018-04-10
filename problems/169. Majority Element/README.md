# 169. Majority Element

## #1 暴力搜索[TLE]

我们可以遍历每个元素，然后判断该元素是否为`majority element`。

```java
class Solution {
    public int majorityElement(int[] nums) {
        int majorityCount = nums.length/2;

        for (int num : nums) {
            int count = 0;
            for (int elem : nums) {
                if (elem == num) {
                    count += 1;
                }
            }

            if (count > majorityCount) {
                return num;
            }

        }

        return -1;    
    }
}
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

## #2 HashMap[AC]

通过一个HashMap数据结构统计每个变量出现的次数，然后变量每个`key-value`对，找出`value`最大对应的`key`。

```java
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            }
            else {
                counts.put(num, counts.get(num)+1);
            }
        }
        return counts;
    }

    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);

        Map.Entry<Integer, Integer> majorityEntry = null;
        for (Map.Entry<Integer, Integer> entry : counts.entrySet()) {
            if (majorityEntry == null || entry.getValue() > majorityEntry.getValue()) {
                majorityEntry = entry;
            }
        }

        return majorityEntry.getKey();
    }
}
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## #3 计数[AC]

该算法被称为 [Boyer–Moore majority vote algorithm](https://www.wikiwand.com/en/Boyer%E2%80%93Moore_majority_vote_algorithm)，用于在线性时间和常量空间内，找出数组中的`majority element`。

```java
class Solution {
    public int majorityElement(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        int count = 1;
        int res = nums[0];
        for(int i=1; i<nums.length; i++){
            if(nums[i] == res)
                count++;
            else{
                count--;
                if(count == 0){
                    count = 1;
                    res = nums[i];
                }
            }
        }
        return res;
    }
}
```

## #4 排序后取中值[AC]

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```

