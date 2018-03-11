#  410. Split Array Largest Sum

## #1 暴力递归[TLE]

```java
class Solution {
    private int ans;
    private int n, m;
    private void dfs(int[] nums, int i, int cntSubarrays, int curSum, int curMax) {
        if (i == n && cntSubarrays == m) {
            ans = Math.min(ans, curMax);
            return;
        }
        if (i == n) {
            return;
        }
        if (i > 0) {
            dfs(nums, i + 1, cntSubarrays, curSum + nums[i], Math.max(curMax, curSum + nums[i]));
        }
        if (cntSubarrays < m) {
            dfs(nums, i + 1, cntSubarrays + 1, nums[i], Math.max(curMax, nums[i]));
        }
    }
    public int splitArray(int[] nums, int M) {
        ans = Integer.MAX_VALUE;
        n = nums.length;
        m = M;
        dfs(nums, 0, 0, 0, 0);
        return ans;
    }
}
```

## #2 动态规划[AC]

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        int[][] f = new int[n + 1][m + 1];
        int[] sub = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                f[i][j] = Integer.MAX_VALUE;
            }
        }
        for (int i = 0; i < n; i++) {
            sub[i + 1] = sub[i] + nums[i];
        }
        f[0][0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                for (int k = 0; k < i; k++) {
                    f[i][j] = Math.min(f[i][j], Math.max(f[k][j - 1], sub[i] - sub[k]));
                }
            }
        }
        return f[n][m];        
    }
}
```



## #3 负相关的二分求解[AC]
  这道题目确实非常有难度，难度点在于对问题的建模，如何找到最大值的最小值val和m的关系，它们之间是一个负相关的关系，也就是val越大，m越小。所有val和m是满足单调递减的函数关系，我们还是可以用二分的方法去猜答案，每次都猜中点，这里还是要用反函数的做法，就是固定m，反向猜val。我们可以将二分法的框架用于这类题目中，我们默认规定的区间是左闭右开的区间，写好guess函数是这道题目的关键，也是所有二分问题的出题点。

```java
public class Solution {
    public boolean guess(long mid, int[] nums, int m){
        long sum = 0;
        for(int i=0; i<nums.length; i++){
            if(nums[i] > mid)
                return false;
            if(sum + nums[i] > mid){
                m--;
                sum = nums[i];
            }else{
                sum += nums[i];
            }
        }
        return m >= 1;
    }
    
    public int splitArray(int[] nums, int m) {
        long low = 0l;
        long high = 1l;
        long mid = 0l;
        int ans = 0;
        for(int i=0; i<nums.length; i++){
            high += nums[i];
        }
        while(low < high){
            mid = (low + high)/2;
            if(guess(mid, nums, m)){
                ans = (int)mid;
                high = mid;
            }else{
                low = mid + 1;
            }
        }
        return ans;
    }
}
```


