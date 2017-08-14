# 46. Permutations

## Description

```
Difficulty: Medium
Total Accepted:175.6K
Total Submissions:402.2K
Contributor: LeetCode
```

Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:

```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

***

## Solution1

  这是一道比较常见的题目，求全排列，容易想到的解法就是回溯的递归求解。做了不少的递归的题目，应该总结一下递归的套路特点：

1. 把和答案相关的变量定义为全局变量
2. 递归函数少不了index这个指标变量
3. 递归函数少不了递归出口，一般就是递归函数的第一个判断语句就用来判断递归出口。
4. 如果需要回溯的递归求解，那么需要加上访问标志。

 目前先总结这么多了，一步一个脚印。

```java
public class Solution {
    private static List<List<Integer>> ans = new ArrayList<List<Integer>>();
    private static int[] path;
    private static boolean[] visit;
    
    public void find(int idx, int[] nums){
        if(idx >= nums.length){
            ArrayList<Integer> arrPath = new ArrayList();
            for(int i=0; i<path.length; i++){
                arrPath.add(nums[path[i]]);
            }
            ans.add(arrPath);
            return;
        }
        for(int i=0; i<nums.length; i++){
            if(!visit[i]){
                visit[i] = true;
                path[idx] = i;
                find(idx+1, nums);
                visit[i] = false;
            }
        }
        return;
    }
    
    public List<List<Integer>> permute(int[] nums) {
        ans.clear();
        visit = new boolean[nums.length];
        path = new int[nums.length];
        find(0,nums);
        return ans;
    }
}
```

***

**enjoy life, coding now! :D**
