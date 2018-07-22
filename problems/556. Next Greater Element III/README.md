# 556. Next Greater Element III

## #1 深度优先遍历[AC]

### 思路

遍历所有可能的情况，然后排序，最后选出第一个大于N的结果。

### 算法

```java
class Solution {
    List<Long> total = new ArrayList<>(); 
    public int nextGreaterElement(int n) {
        String ns = String.valueOf(n);
        int[] nums = new int[10];
        for(int i=0; i<ns.length(); i++){
            nums[ns.charAt(i) - '0']++;
        }
        dfs(nums, 0, ns.length(), new StringBuffer());
        Collections.sort(total);
        // System.out.print(total);
        for(long val : total){
            if(val > n && val < Integer.MAX_VALUE)
                return (int)val;
        }
        return -1;
    }
    
    public void dfs(int[] nums, int step, int length, StringBuffer sb){
        if(step == length){
            total.add(Long.parseLong(sb.toString()));
            return;
        }else{
            for(int i=0; i<nums.length; i++){
                if(nums[i] <= 0)
                    continue;
                sb.append(""+i);
                nums[i]--;
                dfs(nums, step+1, length, sb);
                sb.setLength(sb.length() - 1);
                nums[i]++;
            }
        }
    }
}
```

### 复杂度分析

- 时间复杂度
- 空间复杂度