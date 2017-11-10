# 396. Rotate Function

# Solution

这道题目有两个函数要写，第一个是轮换数组，第二个函数是计算F。

写这两个函数本身没有什么太大的难度，按照题目的要求写的答案如下:

```java
class Solution {
    public int maxRotateFunction(int[] A) {
        //boundary condition
        if(A == null || A.length == 0)
            return 0;
        //normal condition
        int max = Integer.MIN_VALUE;
        for(int i=0; i<A.length; i++){
            int[] B = new int[A.length];
            int F = 0;
            if(i==0) B = A;
            else B = rotating(A, i);
            for(int k=0; k<A.length; k++){
                F += k*B[k];
            }
            max = Math.max(F, max);
        }
        return max;
    }
    
    private int[] rotating(int[] A, int k){
        k = k % A.length;
        int[] left = new int[A.length-k];
        for(int i=0; i<A.length-k; i++){
            left[i] = A[i];
        }
        int[] right = new int[k];
        for(int i=A.length-k; i<A.length; i++){
            right[i-A.length+k] = A[i];
        }
        reverse(left);
        reverse(right);
        int[] result = new int[A.length];
        for(int i=0; i<left.length; i++){
            result[i] = left[i];
        }
        for(int i=0; i<right.length; i++){
            result[i+left.length] = right[i];
        }
        reverse(result);
        return result;
    }
    
    private void reverse(int[] arr){
        for(int i=0, j=arr.length-1; i<j; i++, j--){
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
}
```

但是，结果超时了。看了下答案，给大神跪了，他们发现了Fk和Fk-1之间的规律，然后就可以在O(n)时间内求解。

```java
class Solution {
    public int maxRotateFunction(int[] A) {
        int allSum = 0;
        int len = A.length;
        int F = 0;
        for (int i = 0; i < len; i++) {
            F += i * A[i];
            allSum += A[i];
        }
        int max = F;
        for (int i = len - 1; i >= 1; i--) {
            F = F + allSum - len * A[i];
            max = Math.max(F, max);
        }
        return max;   
    }
}
```

