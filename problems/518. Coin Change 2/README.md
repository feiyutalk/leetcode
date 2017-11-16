# 518. Coin Change 2

# Solution

看到这道题目的第一想法是按照排列组合那种方式去枚举每个硬币可能的数量，由于之前把排列组合的算法模板总结好了，直接套用模板来做就可以了，但是提交之后发现超时了，分析了一下，大概的时间复杂度是O(n^2)，后面再看一下用其他算法能不能把时间复杂度降低。

```java
class Solution {
    private int result;
    public int change(int amount, int[] coins) {
        backtrack(amount, coins, new ArrayList<Integer>(), 0);
        return result;
    }
    
    private void backtrack(int amount, int[] coins, List<Integer> temp, int step){
        int sum = getSum(temp, coins);
        if(sum == amount){
            result+=1;
            return;
        }
        if(sum > amount) return;
        if(temp.size() == coins.length) return;
        
        for(int i=0; i*coins[step]<=amount; i++){
            temp.add(i);
            backtrack(amount, coins, temp, step+1);
            temp.remove(temp.size()-1);
        }
    }
    
    private int getSum(List<Integer> nums, int[] coins){
        int sum = 0;
        for(int i=0; i<nums.size(); i++){
            sum += (nums.get(i) * coins[i]);
        }
        return sum;
    }
}
```

看了一下别人做的，用的动态规划，其实一开始做这道题目的时候有考虑过动态规划，但是发现枚举法也能求解，而且枚举法的模板已经总结好了，写起来会比较的容易，所以就直接用枚举法了。现在想想动态规划要解决的几个问题，一是状态的定义，这里状态的定义就是题目所要求的，只是题目要求的是动态规划最后的状态。二是初始已知的状态，初始已知的状态就是用0种coin，组合出amount为0的个数为1，用i种coin，组合出amount为0的个数为1。

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[][] dp = new int[coins.length + 1][amount + 1];
        dp[0][0] = 1;
        for(int i=1; i<=coins.length; i++){
            dp[i][0] = 1;
            for(int j=1; j<=amount; j++){
                dp[i][j] = dp[i-1][j] + (j>=coins[i-1]?dp[i][j-coins[i-1]]:0);
            }
        }
        return dp[coins.length][amount];
    }
}
```

