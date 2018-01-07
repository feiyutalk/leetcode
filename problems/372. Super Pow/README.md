# 372. Super Pow

```java
class Solution {
    int DIV = 1337;
    
    List<Integer> findLoop(int a){
        List<Integer> index = new ArrayList<>();
        boolean[] set = new boolean[DIV];
        int rem = a % DIV;
        while ( ! set[rem] ) {
            set[rem]=true;
            index.add(rem);
            rem = (rem*a) % DIV;
        }
        return index;
    }
    
    int modBy(int[] b, int m){
        int rem = 0;
        for (int i=0; i < b.length; i++) {
            rem = (rem*10+b[i]) % m;
        }
        return rem;
    }

    public int superPow(int a, int[] b) {
        if (a==0 || a==DIV || b==null || b.length == 0) return 0;
        if (a==1) return 1;
        if (a > DIV) return superPow( a % DIV, b);
        List<Integer> index = findLoop(a);
        int loopsize = index.size();
        int rem = modBy(b, loopsize);
        rem = rem==0? loopsize: rem;
        return index.get(rem-1);
    }
}
```

