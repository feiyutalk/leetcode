# 402. Remove K Digits
## #1 暴力搜索[TLE]

我们可以暴力搜索每一种解空间，具体的搜索方式如下：**对于每一个元素，我们有两种选择方式，删除或者不删除，依次对每个元素进行这两种选择，总共可以得到$O(2^n)$种可能的解，在这些所有的解里面挑选出最小的值作为结果返回。**

```java
class Solution {
    String result = "";
    int resVal = Integer.MAX_VALUE;
    public String removeKdigits(String num, int k) {
        if(num == null || num.length() == 0)
            return "0";
        if(k >= num.length())
            return "0";
        helper(num, new boolean[num.length()], k, 0);
        return result;
    }
    
    public void helper(String num, boolean[] removed, int k, int step){
        if(k == 0){
            int curVal = getNum(num, removed);
            if(curVal < resVal){
                resVal = curVal;
                result = getString(num, removed);
            }
            return;
        }
        if(step == num.length())
            if(k == 0){
                int curVal = getNum(num, removed);
                if(curVal < resVal){
                    resVal = curVal;
                    result = getString(num, removed);
                }
                return;
            }else
                return;
        // remove current number
        removed[step] = true;
        helper(num, removed, k-1, step+1);
        removed[step] = false;
        helper(num, removed, k, step+1);
    }
    
    public int getNum(String num, boolean[] removed){
        int res = 0;
        for(int i=0; i<removed.length; i++){
            if(!removed[i]){
                res *= 10;
                res += (num.charAt(i) - '0');
            }
        }
        return res;
    }
    
    public String getString(String num, boolean[] removed){
        String res = "";
        int first = 0;
        while(first<removed.length && (removed[first] || num.charAt(first) == '0'))
            first++;
        for(int i=first; i<removed.length; i++){
            if(!removed[i])
                res += (num.charAt(i));
        }
        return res==""?"0":res;
    }
}
```

#### 复杂性分析:

- **时间复杂性**：$O(n2^n)$
- **空间复杂性：**$O(n)$

## #2 贪心算法[AC]

我们发现这样一种情况，对于输入：`1785,k=1`。我们发现，删除`8`，得到的结果`175`是最小的。即，我们每次都删除第一个下降的元素，即`nums[i] > nums[i+1]`，这样的元素时，得到的结果是最小的。

```java
class Solution {
    public String removeKdigits(String num, int k) {
        int len = num.length();
        //corner case
        if(k==len)        
            return "0";
            
        Stack<Character> stack = new Stack<>();
        int i =0;
        while(i<num.length()){
            //whenever meet a digit which is less than the previous digit, discard the previous one
            while(k>0 && !stack.isEmpty() && stack.peek()>num.charAt(i)){
                stack.pop();
                k--;
            }
            stack.push(num.charAt(i));
            i++;
        }
        
        // corner case like "1111"
        while(k>0){
            stack.pop();
            k--;            
        }
        
        //construct the number from the stack
        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty())
            sb.append(stack.pop());
        sb.reverse();
        
        //remove all the 0 at the head
        while(sb.length()>1 && sb.charAt(0)=='0')
            sb.deleteCharAt(0);
        return sb.toString();
    }
}
```

