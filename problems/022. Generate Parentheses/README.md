# 22. Generate Parentheses

## #1 产生全集，然后过滤

### 思路

先产生所有可能的组合情况，然后对每种情况做判断，筛选出符合情况的字符串。

### 算法

```java
class Solution {
    private Set<String> set = new HashSet<>();
    public List<String> generateParenthesis(int n) {
        if(n < 1)
            return new ArrayList<String>();
        generateAll(n, n, 0, n, new StringBuffer());
        List<String> res = new ArrayList<>();
        for(String s : set){
            if(isValid(s))
                res.add(s);
        }
        return res;
    }
    
    public void generateAll(int ln, int rn, int step, int n, StringBuffer sb){
        if(step == 2*n){
            set.add(sb.toString());
            return;
        }
        // ln > 0 的情况下
        if(ln > 0){
            sb.append("(");
            generateAll(ln-1, rn, step+1, n, sb);
            sb.deleteCharAt(sb.length() - 1);
            if(rn > 0){
                sb.append(")");
                generateAll(ln, rn-1, step+1, n, sb);
                sb.deleteCharAt(sb.length() - 1);
            }
        }else{ // rn > 0
            sb.append(")");
            generateAll(ln, rn-1, step+1, n, sb);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
    
    public boolean isValid(String s) {
        if(s == null || s.length() == 0)
            return true;
        char first = s.charAt(0);
        if(first == '}' || first == ')' || first == ']')
            return false;
        Stack<Character> stack = new Stack<>();
        stack.push(first);
        for(int i=1; i<s.length(); i++){
            char cur = s.charAt(i);
            if(cur == '{' || cur == '[' || cur == '(')
                stack.push(cur);
            else{
                if(stack.isEmpty()) return false;
                if(cur == '}'){
                    if(stack.pop() != '{') return false;
                }else if(cur == ']'){
                    if(stack.pop() != '[') return false;
                }else if(cur == ')'){
                    if(stack.pop() != '(') return false;
                }else{
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```

### 复杂性分析

- 时间复杂性
- 空间复杂性

