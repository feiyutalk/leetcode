# 338. Counting Bits

# Description

Given a non negative integer number **num**. For every numbers **i** in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example:**
For `num = 5` you should return `[0,1,1,2,1,2]`.

**Follow up:**

- It is very easy to come up with a solution with run time **O(n\*sizeof(integer))**. But can you do it in linear time **O(n)** /possibly in a single pass?
- Space complexity should be **O(n)**.
- Can you do it like a boss? Do it without using any builtin function like **__builtin_popcount** in c++ or in any other language.

# Solution

这道题目，是关于bit操作的题目，bit操作，还不是很熟悉，这里要求出递增数值的bit表示中，1的个数。把答案抄上了，感觉还是迷迷糊糊，找个时间好好总结一下。

```java
class Solution {
    public int[] countBits(int num) {
        int[] ret = new int[num+1];
        ret[0] = 0;
        int pow = 1;
        for(int i=1, t=0; i<=num; i++, t++){
            if(i == pow){
                pow *= 2;
                t = 0;
            }
            ret[i] = ret[t] + 1;
        }
        return ret;
    }
}
```

