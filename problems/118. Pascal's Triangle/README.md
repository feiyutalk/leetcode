# 118. Pascal's Triangle

# Solution

这道题目，这边主要是要发现当前的数组的构造要用到上一次数组信息，构造的过程可以看代码，不难理解。

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> first = new ArrayList<>(Arrays.asList(new Integer[]{1}));
        List<Integer> second = new ArrayList<>(Arrays.asList(new Integer[]{1,1}));
        //boundary condition
        if(numRows <= 0) return result;
        if(numRows == 1){
            result.add(first);
            return result;
        }
        if(numRows == 2){
            result.add(first);
            result.add(second);
            return result;
        }
        result.add(first);
        result.add(second);
        //normal condition     
        for(int i=3; i<=numRows; i++){
            List<Integer> temp = new ArrayList<>();
            List<Integer> last = result.get(result.size()-1);
            temp.add(1);
            for(int j=1; j<last.size(); j++){
                temp.add(last.get(j)+last.get(j-1));
            }
            temp.add(1);
            result.add(temp);
        }
        return result;
    }
}
```

