# 67. Add Binary

## #1 进位相加

### 思路

整数加法本身不是特别难的问题，但是因为采用不同的存储方式来表示整数，导致我们在写整数加法的时候需要特别处理，`LeetCode`上关于整数表示方式有：链表、数组、字符串。解决这类问题的基本思路都是从低位开始遍历，通过进位相加法来处理相加后每一位得到的结果。

### 算法

```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuffer sb = new StringBuffer();
        int i = a.length()-1;
        int j = b.length() - 1;
        int carry = 0;
        while(i >= 0 || j >=0){
            int sum = carry;
            if(i>=0) sum+=a.charAt(i--) - '0';
            if(j>=0) sum+=b.charAt(j--) - '0';
            sb.append(sum%2);
            carry = sum/2;
        }
        if(carry!=0) sb.append(carry);
        return sb.reverse().toString();
    }
}
```

### 复杂度分析：

- 时间复杂性：$O(n)$
- 空间复杂性：$O(1)$

