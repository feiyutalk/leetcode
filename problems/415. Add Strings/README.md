# 415. Add Strings

```java
class Solution {
    public String addStrings(String num1, String num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        if(len1 > len2){
            String tmp = num1;
            num1 = num2;
            num2 = tmp;
        }
        int diff = num2.length() - num1.length();
        while(diff > 0){
            num1 = "0" + num1;
            diff--;
        }
        int carry = 0;
        StringBuffer sb = new StringBuffer();
        for(int j=num1.length()-1; j>=0; j--){
            int sum = (num1.charAt(j) - '0' + num2.charAt(j) - '0' + carry)%10;
            carry = (num1.charAt(j) - '0' + num2.charAt(j) - '0' + carry)/10;
            sb.insert(0, sum);
        }
        if(carry != 0)
            sb.insert(0, carry);
        return sb.toString();
    }
}
```



