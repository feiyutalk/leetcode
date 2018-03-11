# 357. Count Numbers with Unique Digits

# #1 递归[AC]

这道题目最开始的想法就是想采用类似于计算排列组合的时候用到的递归和回溯的方法，但是和排列组合稍微有点不同的是，数值的首位为0没意义，所以对于首位，我们需要单独的处理，就是在主函数中，进行首位的单独循环，做题的时候，大致的思路是对的，但是不知道哪里搞错了，调了半天，最后直接上了别人的答案。

```java
class Solution {
    private int count = 0;
    public int countNumbersWithUniqueDigits(int n) {
        //boundary condition
        if(n == 0)
            return 1;
        if(n > 10)
            return countNumbersWithUniqueDigits(10);
        
        //normal condition
        int count = 1;//x == 0
        long max = (long) Math.pow(10, n);
        
        boolean[] used = new boolean[10];
        for(int i=1; i<10; i++){
            used[i] = true;
            count += backtrack(i, max, used);
            used[i] = false;
        }
        return count;
    }
    
    private int backtrack(long prev, long max, boolean[] used){
        int count = 0;
        if(prev < max){
            count++;
        }else{
            return count;
        }
        for(int i=0; i<10; i++){
            if(used[i])
                continue;
            used[i] = true;
            long cur = 10 * prev + i;
            count += backtrack(cur, max, used);
            used[i] = false;
        }
        return count;
    }
}
```

