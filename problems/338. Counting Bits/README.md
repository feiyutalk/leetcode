# 338. Counting Bits

## #1 暴力搜索[AC]

### 思路

我们需要算法`0<=i<=num`这个范围内，每个数中有几个1，最直接的想法当然是遍历这个范围内的所有数值，然后求解这个数值有几个1。

### 算法

```java
class Solution {
    public int[] countBits(int num) {
        int[] res = new int[num+1];
        for(int i=0; i<res.length; i++){
            int count = 0;
            int val = i;
            for(int j=0; j<32; j++){
                if((val & 1) == 1)
                    count++;
                val >>= 1;
            }
            res[i] = count;
        }
        return res;
    }
}
```

此外，我们还可以通过`x&=(x-1)`消除最后一个1的方式来统计`x`中到底有多少个1。

```java
    private int popcount(int x) {
        int count;
        for (count = 0; x != 0; ++count)
          x &= x - 1; //zeroing out the least significant nonzero bit
        return count;
    }
```

### 复杂性分析

- 时间复杂性：$O(n*sizeof(interger))$
- 空间复杂性：$O(n)$

## #2 动态规划（高位添1）[AC]

### 思路

通过观察二进制数的特点，我们发现可以在某个数a的二进制前面添1来得到更大的数b，而b中1的数量比a多1。比如：

$$\begin{align} (0) &= (0)_2 \\  (1) &= (1)_2 \\  (2) &= (10)_2 \\  (3) &= (11)_2 \\ \end{align}$$

我们发现，在数值$0$的二进制前面加1，会得到$3$，而3二进制表示法中1的个数比0的二进制表示法中1的个数多1。

我们记$P(x)$表示x的二进制表示法中1的个数，于是，我们得到如下的表示式子：

$$P(x+b) = P(x) + 1, b=2^m > x$$

基于这个表达式，我们可以设计出动态规划的算法来求解。

### 算法

```java
public class Solution {
    public int[] countBits(int num) {
        int[] ans = new int[num + 1];
        int i = 0, b = 1;
        // [0, b) is calculated
        while (b <= num) {
            // generate [b, 2b) or [b, num) from [0, b)
            while(i < b && i + b <= num){
                ans[i + b] = ans[i] + 1;
                ++i;
            }
            i = 0;   // reset i
            b <<= 1; // b = 2b
        }
        return ans;
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## #3 动态规划（最低位消1）[AC]

### 思路

想法和上面的类似，只是我们利用了`x&(x-1)`会去掉最后一个1的技巧，来重写我们的转移方程：

$$P(x+b) = P(x \& (x-1)) + 1$$

### 算法

```java
public class Solution {
  public int[] countBits(int num) {
      int[] ans = new int[num + 1];
      for (int i = 1; i <= num; ++i)
        ans[i] = ans[i & (i - 1)] + 1;
      return ans;
  }
}
```

### 复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

