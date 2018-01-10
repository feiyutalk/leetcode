# 484. Find Permutation

```java
class Solution {
    public int[] findPermutation(String s) {
        if(s == null || s.length() == 0) return new int[0];
        int n = s.length();
        int[] res = new int[n+1];
        // sorted
        for(int i=0; i<res.length; i++){
            res[i] = i+1;
        }
        // reveres when 'D'
        for(int h=0; h<s.length(); h++){
            if(s.charAt(h) == 'D'){
                int l = h;
                while(h < s.length() && s.charAt(h) == 'D') h++;
                reverse(res, l, h);
            }
        }
        return res;
    }
    
    private void reverse(int[] res, int l, int h){
        while(l < h){
            int temp = res[l];
            res[l] = res[h];
            res[h] = temp;
            l++;h--;
        }
    }
}
```

