# 66. Plus One

## #1 翻转数组+进位相加[AC]

### 思路

该题用数组这种结构来表示整数，整数的最低位是反而是数组下标的最高位`length-1`，整数的最高位是数组下标的最低位`0`。这样处理起来可能会比较麻烦，我们可以先对数组进行翻转，使得数组的低位对应整数表示的低位，数组的高位对应整数表示的高位，然后进行进位相加。最后，在返回结果前，对结果数组进行翻转。

### 算法

```java
class Solution {
    public int[] plusOne(int[] digits) {
        if(digits == null || digits.length == 0)
            return new int[0];
        // first bit
        reverse(digits);
        int sum = digits[0] + 1;
        digits[0] = sum % 10;
        int carry = sum / 10;
        for(int i=1; i<digits.length; i++){
            if(carry == 0)
                break;
            sum = digits[i] + carry;
            digits[i] = sum % 10;
            carry = sum / 10;
        }
        if(carry == 0){
            reverse(digits);
            return digits;
        }
        int[] res = new int[digits.length + 1];
        for(int i=0; i<digits.length; i++)
            res[i] = digits[i];
        res[digits.length] = carry;
        reverse(res);
        return res;
    }
    
    public void reverse(int[] nums){
        for(int i=0,j=nums.length-1; i<j; i++,j--){
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
            
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

