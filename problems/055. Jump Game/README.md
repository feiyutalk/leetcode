# 55. Jump Game

## #1 暴力搜索[TLE]

在每个位置上，我们可以遍历下一次可以走的每个位置，这个范围为`[step+1, step+nums[step])]`，如果最后`step >= nums.length - 1`说明是可以走到终点的；如果遍历完所有的范围都不行， 那说明不能走到终点。

```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        return helper(nums, 0);
    }
    
    private boolean helper(int[] nums, int step){
        if(step >= nums.length - 1)
            return true;
        int furtherst = Math.min(step+nums[step], nums.length-1);
        for(int i=step+1; i<=furtherst; i++){
            if(helper(nums, i))
                return true;
        }
        return false;
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n^2)$
- **空间复杂性：**$O(n)$

## #2 动态规划+自顶向下[SOF]

我们可以定义一个缓存数组来保存我们每一次搜索的情况，下次在计算之前可以先查看缓存中是否有该值，如果有就直接从缓存中取，否则进行计算，然后将结果存入到缓存中。

```java 
class Solution {
    Boolean [] memo;
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        memo = new Boolean[nums.length];
        return helper(nums, 0);
    }
    
    private boolean helper(int[] nums, int step){
        if(step >= nums.length - 1)
            return true;
        if(memo[step] != null)
            return memo[step];
        int furtherst = Math.min(step+nums[step], nums.length-1);
        for(int i=step+1; i<=furtherst; i++){
            if(helper(nums, i)){
                memo[step] = true;
                return true;
            }
        }
        memo[step] = false;
        return false;
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n^2)$
- **空间复杂性：**$O(2n)=O(n)$

## #3 动态规划-自底向上[TLE]

从上面一种解法中，我们可以看到，我们利用缓存存储了计算结果，采用自顶向下的编程方式，现在我们考虑采用自底向上的编程方式，将后续需要用到的结果先计算并存储起来，我们称之为状态，然后利用状态转移方程进行未知状态向已知状态的转化。转移方程为:

```java
        int furtherst = Math.min(step+nums[step], nums.length-1);
        for(int i=step+1; i<=furtherst; i++){
            if(helper(nums, i)){
                memo[step] = true;
                return true;
            }
        }
```

完整代码如下:

```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        boolean[] dp = new boolean[nums.length];
        dp[nums.length - 1] = true;
        for(int i=nums.length-2; i>=0; i--){
            int far = Math.min(i + nums[i], nums.length-1);
            for(int j=i+1; j<=far; j++){
                if(dp[j]){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[0];
    }
}
```

## #4 贪心[AC]

从上面的自顶向上的编程模式中(在本题中，相当于从右边向左边计算)，我们进一步思考，能否继续优化呢？

首先，我们可以看到，对于每个位置是否可达，我们从`[i+1, i+nums[i]]`依次遍历，它的下一步是否可达，但是在代码中我们发现，只要在`[i+1, i+nums[i]]`中存在一个可达的位置，则当前位置就可达，我们从`break`这个语句中也可以说明这一点。所有，我们只要用一个变量记录当前最左可达位置`lastLeftPos`，然后对于当前位置，判断`i+nums[i] >= lastLeftPos`是否满足，如果满足，说明当前位置是可达的，否则是不可达的。

我们从暴力搜索到动态规划到贪心算法，得到了什么启示呢？我们可以发现，暴力搜索的想法是最直接的，通过枚举所有可能的解空间，就可以得到最终的结果，我们一般时候递归的方式来编写暴力搜索的过程，但是，暴力搜索算法会带来冗余计算（这在递归函数里表现为同样参数的函数结果会被多次计算），所以我们引进缓存，来记录下已经计算过的结果（即参数相同的递归函数结果值），这样做已经是动态规划算法了，只是我们一般用自底向上的方式来编写动态规划函数，这时候我们就需要定义状态、初始状态和转移方程，然后从开始状态一步一步的求解到最终的状态。在动态规划算法中，其转移方程表示的是未知的状态值向已知状态值的转移路径，而这个转移路径都是有多条可能的路径的（在本题中就表现为我们要判断当前的位置状态值，需要去搜索`[i+1, i+nums[i]]`这些位置的所有路径的状态值)。所以我们发现，在转移方程的过程中，一般都涉及到枚举比较每一种可能路径的值，从中取得最路径值。而对这个转移过程进一步优化就是贪心算法的本质，贪心算法通过观察问题的主要矛盾，从而可直接从多种路径得到最优值。

```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        int lastLeftPos = nums.length - 1;
        for(int i=nums.length-1; i>=0; i--)
            if(i + nums[i] >= lastPos)
                lastLeftPos = i;
        return lastLeftPos == 0;
    }
}
```

