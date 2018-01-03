# 491. Increasing Subsequences

```java
class Solution {
     public List<List<Integer>> findSubsequences(int[] nums) {
         Set<List<Integer>> res= new HashSet<List<Integer>>();
         List<Integer> holder = new ArrayList<Integer>();
         findSequence(res, holder, 0, nums);
         List result = new ArrayList(res);
         return result;
     }

    public void findSequence(Set<List<Integer>> res, List<Integer> holder, int index, int[] nums) {
        if (holder.size() >= 2) {
            res.add(new ArrayList(holder));
        }
        for (int i = index; i < nums.length; i++) {
            if(holder.size() == 0 || holder.get(holder.size() - 1) <= nums[i]) {
                holder.add(nums[i]);
                findSequence(res, holder, i + 1, nums);
                holder.remove(holder.size() - 1);
            }
        }
    }
}
```

