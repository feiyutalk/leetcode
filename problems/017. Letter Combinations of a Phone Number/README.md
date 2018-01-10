# 017. Letter Combinations of a Phone Number

```java
class Solution {
    private List<String> res = new ArrayList<String>();
    private Map<Character, String> letters = new HashMap<>();
    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.length() == 0) return new ArrayList<String>();
        letters.put('0', "");
        letters.put('1', "");
        letters.put('2', "abc");
        letters.put('3', "def");
        letters.put('4', "ghi");
        letters.put('5', "jkl");
        letters.put('6', "mno");
        letters.put('7', "pqrs");
        letters.put('8', "tuv");
        letters.put('9', "wxyz");
        helper(digits, "", 0, digits.length());
        return res;
    }
    
    private void helper(String digits, String temp, int loc, int n){
        if(temp.length() == n){
            res.add(new String(temp));
            return;
        }
        for(Character c : letters.get(digits.charAt(loc)).toCharArray()){
            temp += ("" + c);
            helper(digits, temp, loc+1, n);
            temp = temp.substring(0, temp.length()-1);
        }
    }
}
```

