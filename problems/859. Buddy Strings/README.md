# 859. Buddy Strings

## #1 暴力搜索[TLE]

### 思路

### 算法

```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        if(A == null || A.length() == 0) return false;
        if(B == null || B.length() == 0) return false;
        if(A.length() != B.length()) return false;
        for(int i=0; i<A.length()-1; i++){
            for(int j=i+1; j<B.length(); j++){
                //判断两个字符串是否相同
                boolean find = true;
                for(int k=0; k<A.length(); k++){
                    if(k == i){
                        if(A.charAt(j) != B.charAt(k)){
                            find = false;
                            break;
                        }
                    }else if(k == j){
                        if(A.charAt(i) != B.charAt(k)){
                            find = false;
                            break;
                        }
                    }else{
                        if(A.charAt(k) != B.charAt(k)){
                            find = false;
                            break;
                        }
                    }
                }
                if(find)
                    return true;
            }
        }
        return false;
    }
}
```

## #2 Enumerate Cases

### 思路

Let's say `i` is *matched* if `A[i] == B[i]`, otherwise `i` is *unmatched*. A buddy string has almost all matches, because a swap only affects two indices.

If swapping `A[i]` and `A[j]` would demonstrate that `A` and `B` are buddy strings, then `A[i] == B[j]` and `A[j] == B[i]`. That means among the four free variables `A[i], A[j], B[i], B[j]`, there are only two cases: either `A[i] == A[j]` or not.

### 算法

Let's work through the cases.

In the case `A[i] == A[j] == B[i] == B[j]`, then the strings `A` and `B` are equal. So if `A == B`, we should check each index `i` for two matches with the same value.

In the case `A[i] == B[j], A[j] == B[i], (A[i] != A[j])`, the rest of the indices match. So if `A` and `B`have only two unmatched indices (say `i` and `j`), we should check that the equalities `A[i] == B[j]` and `A[j] == B[i]` hold.

```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        if (A.length() != B.length()) return false;
        if (A.equals(B)) {
            int[] count = new int[26];
            for (int i = 0; i < A.length(); ++i)
                count[A.charAt(i) - 'a']++;

            for (int c: count)
                if (c > 1) return true;
            return false;
        } else {
            int first = -1, second = -1;
            for (int i = 0; i < A.length(); ++i) {
                if (A.charAt(i) != B.charAt(i)) {
                    if (first == -1)
                        first = i;
                    else if (second == -1)
                        second = i;
                    else
                        return false;
                }
            }

            return (second != -1 && A.charAt(first) == B.charAt(second) &&
                    A.charAt(second) == B.charAt(first));
        }
    }
}
```

### 复杂度分析

- Time Complexity: $O(N)$, where $N$ is the length of `A` and `B`.
- Space Complexity: $O(1)$. 