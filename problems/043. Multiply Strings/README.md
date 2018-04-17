# 43. Multiply Strings

## #1 转化为字符串做乘法[AC]

### 思路

我们需要弄清楚如何做乘法运算，只有弄清楚了乘法运算之后才能比较好的求解这道题目。对于长度为`m`和长度为`n`的两个字符串数字相乘，我们得到的结果字符串的长度最多为`m+n`，然后我们考虑`num[i]`和`num[j]`相乘的结果应该放在哪个位置呢？相乘后的结果取余数和取模应该会被放在`[i+j,i+j+1]`的位置，看下图就明白了：

![stock-photo-130178585](../../../../../../../Desktop/stock-photo-130178585.jpg)

### 算法

```java
class Solution {
    public String multiply(String num1, String num2) {
        int n = num1.length();
        int m = num2.length();
        int[] res = new int[m+n];
        for(int i=n-1; i>=0; i--){
            for(int j=m-1; j>=0; j--){
                int pos1 = i+j;
                int pos2 = i+j+1;
                int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                int sum = mul + res[pos2];
                res[pos2] = sum % 10;
                res[pos1] += sum / 10;
            }
        }
        StringBuffer sb = new StringBuffer();
        for(int val : res){
            if(!(sb.length() == 0 && val == 0))
                sb.append(val);
        }
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(nm)$
- 空间复杂度：$O(m+n)$

