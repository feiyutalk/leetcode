# 60. Permutation Sequence

## #1 回溯法[TLE]

### 思路

采用深度优先递归遍历，用一个数组记录已经采用的数字，当递归深度大于n的时候，就把结果保存下来，时间复杂度太高。

### 算法

```java
class Solution {
    private List<String> res = new ArrayList<>();
    public String getPermutation(int n, int k) {
        boolean[] used = new boolean[n+1];
        backtrack(n, used, new StringBuffer(), 1);
        return res.get(k-1);
    }
    
    public void backtrack(int n, boolean[] used, StringBuffer sb, int step){
        if(step == n+1){
            res.add(sb.toString());
        }
        for(int i=1; i<=n; i++){
            if(!used[i]){
                used[i] = true;
                sb.append(i);
                backtrack(n, used, sb, step+1);
                sb.deleteCharAt(sb.length()-1); 
                used[i] = false;
            }
        }
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(n!)$
- 空间复杂度：$O(n)$

## #2 [AC]

### 算法

```java
public class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        ArrayList<Integer> num = new ArrayList<Integer>();
        int fact = 1;
        for (int i = 1; i <= n; i++) {
            fact *= i;
            num.add(i);
        }
        for (int i = 0, l = k - 1; i < n; i++) {
            fact /= (n - i);
            int index = (l / fact);
            sb.append(num.remove(index));
            l -= index * fact;
        }
        return sb.toString();
    }
}
```

