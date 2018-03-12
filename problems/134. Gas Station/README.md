# 134. Gas Station

## #1 暴力搜索[TLE]

比较直接的想法就是枚举出所有的起始位置，并且判断每一个起始位置是否可以成功的环绕一圈。通过递归的方式来实现。

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if(gas == null || gas.length == 0)
            return -1;
        for(int i=0; i<gas.length; i++){
            if(helper(gas, i, 0, 0, cost))
                return i;
        }
        return -1;
    }
    
    public boolean helper(int[] gas, int index, int remain, int count, int[] cost){
        if(count == gas.length)
            return remain >= 0;
        if(remain < 0)
            return false;
        return helper(gas, (index+1)%gas.length, remain+gas[index]-cost[index], count+1, cost);
    }
}
```

## #2 动态规划(自顶向下)[TLE]

在上面的暴力搜索方法里，可以会涉及到重叠子问题的冗余计算，我们通过一个缓存来存储已经计算过的状态值，避免重复计算。

```java
class Solution {
    Boolean memo[][][];
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if(gas == null || gas.length == 0)
            return -1;
        int sum = 0;
        for(int c : cost)
            sum += c;
        memo = new Boolean[gas.length][sum+1][gas.length];
        for(int i=0; i<gas.length; i++){
            if(helper(gas, i, 0, 0, cost))
                return i;
        }
        return -1;
    }
    
    public boolean helper(int[] gas, int index, int remain, int count, int[] cost){
        if(count == gas.length)
            return remain >= 0;
        if(remain < 0)
            return false;
        if(memo[index][remain][count] != null)
            return memo[index][remain][count];
        boolean res = helper(gas, (index+1)%gas.length, remain+gas[index]-cost[index], count+1, cost);
        memo[index][remain][count] = res;
        return res;
    }
}
```

## #3 动态规划(自底向上)[TLE]

我们可以计算到达每个位置的时候需要的最少`remain`是多少，然后从后往前计算，最后判断`gas[i]-cost[i]>=remain[(i+1+N)%N]`是否成立。

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        if(gas == null || gas.length == 0)
            return -1;
        int N = gas.length;
        int[] remain = new int[N];
        for(int i=0; i<N; i++){
            remain[i] = 0;
            int j = (i-1+N)%N;
            while(j != i){
                remain[j] = Math.max(0, cost[j] - gas[j] + remain[(j+1+N)%N]);
                // System.out.println(j + " " + remain[j]);
                j = (j-1+N) % N;
            }
            if(gas[i] - cost[i] >= remain[(i+1+N)%N])
                return i;
        }
        return -1;
    }
}
```

## #4 贪心[AC]

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int sumGas = 0;
        int sumCost = 0;
        int start = 0;
        int tank = 0;
        for (int i = 0; i < gas.length; i++) {
            sumGas += gas[i];
            sumCost += cost[i];
            tank += gas[i] - cost[i];
            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }
        if (sumGas < sumCost) {
            return -1;
        } else {
            return start;
        }
    }
}
```

