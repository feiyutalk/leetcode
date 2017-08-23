# 394. Decode String

## Description

```
Difficulty: Medium
Total Accepted:33.2K
Total Submissions:80.4K
Contributor: LeetCode
```

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].


**Examples:**

```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

***

## Solution1 转化为栈
  这道题花了我很多时间，一开始就知道要用栈去解决这问题，但是中间还是有很多很多的细节没有考虑到，主要的细节如下：

+ 嵌套
+ 数字可能是十位百位等，不单单只是个位
+ 出栈后的顺序问题

 :tired_face:被这道题整了一个多小时，最后算是AC了，但是感觉自己写得不是很好，慢慢来吧，这道题从问题本质上是很轻易能发现和栈的本质是一样的，但是实现的细节确实需要花费很多时间。

```java
public class Solution {
    public String decodeString(String s) {
        Stack stack = new Stack();
        Stack reStack = new Stack();
        Stack numReStack = new Stack();
        StringBuffer result = new StringBuffer();
        
        char[] chars = s.toCharArray();
        for(int i=0; i<chars.length; i++){
            char cur = chars[i];
            char inChar;
            reStack.clear();
            if(cur == ']'){
                
                do{
                    inChar = (char)stack.pop();
                    if(inChar != '[')
                       reStack.push(inChar);
                }while(inChar != '[');
                // char num = (char)stack.pop();
                
                char numChar;
                do{
                    numChar = (char)stack.pop();
                    if(isNumber(numChar)){
                        numReStack.push(numChar);
                    }else{
                        stack.push(numChar);
                    }
                }while(isNumber(numChar) && !stack.isEmpty());
                
                StringBuffer number = new StringBuffer();
                while(!numReStack.isEmpty()){
                    number.append(numReStack.pop());
                }
                int num = Integer.valueOf(number.toString());
                
                char[] inside = new char[reStack.size()];
                for(int k =0; k<inside.length; k++){
                    inside[k] = (char)reStack.pop();
                }
                for(int j=0; j< num; j++){
                    for(int m=0; m<inside.length; m++){
                        stack.push(inside[m]);
                    }    
                }
            }else{
                stack.push(cur);
            }
        }
        reStack.clear();
        while(!stack.isEmpty()){
            reStack.push(stack.pop());
        }
        
        while(!reStack.isEmpty()){
            result.append(reStack.pop());
        }
        return result.toString();
    }
    
    public boolean isNumber(char c){
        if(c == '0' ||
           c == '1' ||
           c == '2' ||
           c == '3' ||
           c == '4' ||
           c == '5' ||
           c == '6' ||
           c == '7' ||
           c == '8' ||
           c == '9' )
           return true;
         return false;
    }
    
}
```

***

**enjoy life, coding now! :D**
