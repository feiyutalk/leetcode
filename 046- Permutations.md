# Description

:star2::star2:

![](/images/Permutations.png)

***
## Analysis
这是一道比较常见的题目，求全排列，容易想到的解法就是回溯的递归求解。做了不少的递归的题目，应该总结一下递归的套路特点：

1. 把和答案相关的变量定义为全局变量
2. 递归函数少不了index这个指标变量
3. 递归函数少不了递归出口，一般就是递归函数的第一个判断语句就用来判断递归出口。
4. 如果需要回溯的递归求解，那么需要加上访问标志。

目前先总结这么多了，一步一个脚印，算法基础还是差，今天看视频，那老师说了句，记得很多年前写的八皇后，大概是小学还是初中吧。。。。。。。所以，今后还要更加努力才行！毕竟起步晚呐。。

## Solution 带回溯的递归求解

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
enjoy life, coding now! :D