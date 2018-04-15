# 476. Number Complement

## #1 位操作

### 思路

根据题意，我们需要对输入按位进行翻转，但是翻转的区间为：[最高位1的位置，0]，例如输入为5（其二进制表示为`101`），则最高位1的位置是3，所以，我们需要翻转的区间是[3,0]。

为了实现这个算法，我们需要两个步骤：

1. 创建一个包含区间为[最高位1的位置，0]的全是1的mask，对于输入5来说，其mask就是
2. 输入 异或 mask。

### 算法

```java
class Solution {
    public int findComplement(int num) {
        int mask = (Integer.highestOneBit(num) << 1) - 1;
        return num ^ mask;
    }
}
```

