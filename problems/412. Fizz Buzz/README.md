# 412. Fizz Buzz

直接一次循环，在循环中判断该值符合哪个条件，然后进行相应的操作就可以了。

```java
class Solution {
    public List<String> fizzBuzz(int n) {
        if(n == 0) return new ArrayList<String>();
        List<String> res = new ArrayList<>();
        for(int i=1; i<=n; i++){
            if(i % 3 == 0 && i % 5 == 0){
                res.add("FizzBuzz");
            }else if(i % 3 == 0){
                res.add("Fizz");
            }else if(i % 5 == 0){
                res.add("Buzz");
            }else{
                res.add(i+"");
            }
        }
        return res;
    }
}
```

