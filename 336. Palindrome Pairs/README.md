# 336. Palindrome Pairs

# Solution

这道题目，我试了下最简单的解法，就是暴力穷举法，当然了，时间复杂度也就是 O(n3)， 代码如下:

```java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        //boundary condition
        if(words == null || words.length == 0)
            return new ArrayList<List<Integer>>();
        //normal condition
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        for(int i=0; i<words.length; i++){
            for(int j=0; j<words.length; j++){
                if(i == j) continue;
                if(isPalindromePairs(words[i], words[j])){
                    result.add(Arrays.asList(new Integer[]{i, j}));
                }
            }
        }
        return result;
    }
    
    private boolean isPalindromePairs(String w1, String w2){
        String pair = w1 + w2;
        for(int i=0, j=pair.length()-1; i<j; i++, j--){
            if(pair.charAt(i) != pair.charAt(j)) return false;
        }
        return true;
    }
}
```

当然了，结果超时是肯定的了，一般时间复杂度超过O(n2)的时候就要考虑优化算法了，这道题优化的角度当然要改用其他的算法来求解才能减少时间复杂度。

看了一下别人的解法，首先是用一个Map来保存每个字符串的逆序与对应的下标，用到逆序的原因在于如果两个字符串拼接起来能够成为回文，那么他们是逆序关系。这也是分析到了问题的关键点，利用这个点写出更优化的算法。通常来说，暴力求解法都是没有用到任何关键信息的。

```java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        //boundary condition
        if(words == null || words.length < 2)
            return new ArrayList<List<Integer>>();
        //normal condition
        List<List<Integer>> result = new ArrayList<>();
        Map<String, Integer> map = new HashMap<>();
        for(int i=0; i<words.length; i++){
            map.put(new StringBuilder(words[i]).reverse().toString(), i);
        }
        if(map.containsKey("")){
            for(int i=0; i<words.length; i++){
                if(i == map.get("")) continue;
                if(isPalindrome(words[i])) result.add(Arrays.asList(new Integer[]{map.get(""), i}));
            }
        }
        for(int i=0; i<words.length; i++){
            for(int j=0; j<words[i].length(); j++){
                String left = words[i].substring(0, j);
                String right = words[i].substring(j);
                if(map.containsKey(left) && isPalindrome(right) && map.get(left) != i){
                    result.add(Arrays.asList(new Integer[]{i, map.get(left)}));
                }
                if(map.containsKey(right) && isPalindrome(left) && map.get(right) != i){
                    result.add(Arrays.asList(new Integer[]{map.get(right), i}));
                } 
            }
        }
        return result;
    }
    
    private boolean isPalindrome(String word){
        for(int i=0, j=word.length()-1; i<j; i++, j--){
            if(word.charAt(i) != word.charAt(j)) return false;
        }
        return true;
    }
}
```

