# 440. K-th Smallest in Lexicographical Order

# Description

Given integers `n` and `k`, find the lexicographically k-th smallest integer in the range from `1` to `n`.

Note: 1 ≤ k ≤ n ≤ 109.

**Example:**

```
Input:
n: 13   k: 2

Output:
10

Explanation:
The lexicographical order is [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9], so the second smallest number is 10.
```

# Solution

这道题目的难度比较大，可以将字典排序转化成一颗十进制的十叉树，如下所示:

![](https://leetcode.com/uploads/files/1477293057263-upload-40379731-118a-4753-bed9-1cb372790d4b.png)

然后采用先序遍历的方式，来遍历到一个节点就k-1，当k==0，就可以返回了。但是，参考了答案，用了一种更巧妙的方式来避免了遍历，可以参考该答案，也解释得比较清楚：

[answer](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/discuss/)

最后，代码如下:

```java
class Solution {
    public int findKthNumber(int n, int k) {
        int curr = 1;
        k = k-1;
        while(k>0){
            int steps = calSteps(n, curr, curr+1);
            if(steps <= k){
                curr += 1;
                k -= steps;
            }else{
                curr *= 10;
                k -= 1;
            }
        }
        return curr;
    }
    
    private int calSteps(int n, long n1, long n2){
        int steps = 0;
        while(n1 <= n){
            steps += Math.min(n+1, n2) - n1;
            n1 *= 10;
            n2 *= 10;
        }
        return steps;
    }
}
```

