# 247. Strobogrammatic Number II

## #1 暴力搜索[TLE]

### 思路

遍历所有的可能的n位数值，判断其是否满足`strobogrammatic number`的条件，如果是的话，就加入到结果中。

### 算法

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        // 10^(n-1) -> 10^(n) - 1;
        if(n == 1)
            return new ArrayList<String>(Arrays.asList(new String[]{"0", "1", "8"}));
        List<String> res = new ArrayList<>();

        for(int i=(int)Math.pow(10, n-1); i<=(int)Math.pow(10,n)-1; i++){
            if(isStrobogrammatic(i, n))
                res.add(""+i);
        }
        return res;
    }
    
    public boolean isStrobogrammatic(int vali, int n){
        String val = "" + vali;
        if(n % 2 == 0){
            for(int i=0, j=n-1; i<j; i++, j--){
                if(!isOO(val, i, j) && !isEE(val, i, j) && !isSN(val, i, j) && !isZZ(val, i, j) )
                    return false;
            }      
        }else{
            for(int i=0, j=n-1; i<j; i++, j--){
                if(!isOO(val, i, j) && !isEE(val, i, j) && !isSN(val, i, j) && !isZZ(val, i, j))
                        return false;
                if(!isMidStro(val, n/2))
                    return false;
            }
        }

        return true;
    }
    
    private boolean isMidStro(String val, int mid){
        return val.charAt(mid) == '0' || val.charAt(mid) == '1' || val.charAt(mid) == '8';
    }
    
    private boolean isZZ(String val, int left, int right){
        return val.charAt(left) == '0' && val.charAt(right) == '0';
    }
    
    private boolean isOO(String val, int left, int right){
        return val.charAt(left) == '1' && val.charAt(right) == '1';
    }
    
    private boolean isEE(String val, int left, int right){
        return val.charAt(left) == '8' && val.charAt(right) == '8';
    }
    
    private boolean isSN(String val, int left, int right){
        return  (val.charAt(left) == '6' && val.charAt(right) == '9') || (val.charAt(left) == '9' && val.charAt(right) == '6');
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$

## #2 递归[AC]

### 思路

我们只需要知道`(n-2)`的总的`strobogrammatic number`，然后就可以通过在左右两边添加数值得到`n`的总的`strobogrammatic number`。

### 算法

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        return helper(n, n);
    }

    List<String> helper(int n, int m) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));
        if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));

        List<String> list = helper(n - 2, m);

        List<String> res = new ArrayList<String>();

        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);

            if (n != m) res.add("0" + s + "0");

            res.add("1" + s + "1");
            res.add("6" + s + "9");
            res.add("8" + s + "8");
            res.add("9" + s + "6");
        }

        return res;
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

