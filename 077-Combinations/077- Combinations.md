# 77. Combinations

## Description

```
Difficulty: Medium
Total Accepted:119.8K
Total Submissions:302.5K
Contributor: LeetCode
```

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

***
## Solution1 最大值固定的递归求解
  这道题目其实还是挺有难度的，因为做的题目比较少，总结得也比较少，对于这类递归求解的问题，并不能马上得到解题的思路。关于这道题，我的思路在于固定住最大值，当选定一个最大值，然后就可以递归的求解这个问题了。递归也是一种模式，该模式的特点在于我们不断的缩小问题的规划，但是解题的手段却没有任何的变化，我们一直用相同的手段去求解不同规模的问题，当问题小到一定规模，可以直接得到解时(此时也叫递归的出口)，递归就开始返回，用栈的角度来理解，就是每次调用一次递归方法，就会把它入栈，当递归开始返回的时候，开始出栈。把握住递归的关键还是在于寻找求解该问题的一般方式，然后想方式不断的转化为小规模的递归问题。具体求解方式，看代码。

```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        List<Integer> a = new ArrayList<Integer>();
        recCombine(ans, a, n, k);
        return ans;
    }
    
    public void recCombine(List<List<Integer>> ans, List<Integer> a, int n, int k){
        
        if(k == 0){
            ans.add(new ArrayList(a));
            return;
        }
        
        for(int i=n; i>=1; i--){
            a.add(i);
            recCombine(ans, a, i-1, k-1);
            a.remove(new Integer(i));
        }
    }
}
```

***

**enjoy life, coding now! :D**
