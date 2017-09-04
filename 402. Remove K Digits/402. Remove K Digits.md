# 402. Remove K Digits
## Description

```
Difficulty: Medium
```

Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

Note:

- The length of num is less than 10002 and will be ≥ k.
- The given num does not contain any leading zero.

Example 1:

	Input: num = "1432219", k = 3
	Output: "1219"
	Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

Example 2:

	Input: num = "10200", k = 1
	Output: "200"
	Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
## Solution 1
我们希望数值小的留在高位，这样的话就可以使得最后的结果更小。所以，我们可以使用贪心的算法，我们从数值num的高位依次往低位遍历，如果发现前一个位数，比当前位数的数值大，那么我们可以把前一个位数丢掉。

```java

class Solution {
    public String removeKdigits(String num, int k) {
        //boundary condition
        if(num == null || num.length() == 0 || k<0)
            return "";
        if(k == 0)
            return num;
        if(k == num.length())
            return "0";
        //normal condition
        Stack<Character> stack = new Stack<>();
        for(int i=0; i<num.length(); i++){
            while(k>0 && !stack.isEmpty() && num.charAt(i) < stack.peek()){
                stack.pop();
                k--;
            }
            stack.push(num.charAt(i));
        }
        
        // corner case "22222"
        while(k>0){
            stack.pop();
            k--;
        }
        
        StringBuffer sb = new StringBuffer();
        while(!stack.isEmpty())
            sb.append(stack.pop());
        sb.reverse();
        //corner case "0123"
        while(sb.length()>1 && sb.charAt(0) == '0')
            sb.deleteCharAt(0);
        return sb.toString();
                                
    }
}
```

***

**enjoy life, coding now! :D**
